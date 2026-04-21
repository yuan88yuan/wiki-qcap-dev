# RefCountedBuffer System

The `ZzRefCountedBuffer` system provides a thread-safe mechanism for managing the lifetime of memory buffers and their underlying hardware resources across the SDK.

## ZzRefCountedBuffer (Base)
The base class implements a dual-reference counting scheme:
- **Strong Reference (`_M_use_count`)**: Tracks active usage of the buffer's data. When this reaches zero, the buffer's data is disposed.
- **Weak Reference (`_M_weak_count`)**: Tracks references to the buffer's control structure. The object itself is only deleted when the weak count reaches zero.

### Smart Pointers
- **`ZzRefCountedBufferPtr`**: Manages a weak reference. It ensures the control block stays alive but does not guarantee the data is still available.
- **`ZzRefCountedDataPtrT<T>`**: Provides type-safe access to the data. It increments the strong reference count upon creation (`lock_data`) and decrements it upon destruction (`unlock_data`).

## ZzRefCountedBuffer2 (Extended)
`ZzRefCountedBuffer2` extends the base class to decouple the buffer handle from the actual hardware resource.

- **Resource Tracking**: Introduces `mResourceCount` to track the underlying resource independently.
- **Resource Disposal**: Defines a pure virtual `OnFreeResource()` method, allowing subclasses to implement platform-specific cleanup (e.g., freeing DMA buffers).
- **Templating**: Provides `ZzRefCountedBufferT<T>` to embed data directly for better cache locality.

## qcap2 Encapsulation
In the `qcap2` C API, these classes are encapsulated via an opaque handle `qcap2_rcbuffer_t`.

### API Mapping
| C Function | Internal C++ Implementation | Effect |
| :--- | :--- | :--- |
| `qcap2_rcbuffer_add_ref()` | `weak_add_ref()` | Increments **weak count** |
| `qcap2_rcbuffer_release()` | `weak_release()` | Decrements **weak count** |
| `qcap2_rcbuffer_lock_data()` | `lock_data()` | Increments **strong count** |
| `qcap2_rcbuffer_unlock_data()` | `unlock_data()` | Decrements **strong count** |

**Critical Note**: `add_ref` and `release` in the `qcap2` API only manage the object's lifetime, not the data's. `lock_data` must be used to ensure data validity.

## Integration with ZzRefCountedBufferQueue
The `ZzRefCountedBufferQueue` utilizes this system to implement a high-performance recycling pool:
1. **Storage**: Buffers are stored as weak references.
2. **Recycling**: The queue detours the `pOnFreeResource` callback. When a resource is freed, the callback automatically re-adds the buffer to the queue via `weak_add_ref()`, preventing frequent re-allocations.
