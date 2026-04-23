# ZzDemuxer

`ZzDemuxer` is the core component responsible for separating multimedia streams into individual elementary streams (video and audio).

## Architecture
The `ZzDemuxer` employs a **Backend Pattern**. It serves as a high-level coordinator that manages configuration and output streams, while delegating the actual demuxing logic to a specialized `Backend` implementation.

### Core Responsibilities
- **Stream Management**: Identifies and manages multiple video and audio streams, as well as program information (`ZzProgramInfo`).
- **Input Flexibility**: Supports two modes of operation:
    - **URL Mode**: Fetches data from a specified URL.
    - **Push Mode**: Receives data pushed into the demuxer via `Push(ZzRefCountedBuffer*)`.
- **Synchronization**: Coordinates the timing of output streams to ensure audio-video synchronization.
- **Event Notification**: Uses `ZzEvent2` to notify consumers when new packets are available.

## Backends
The demuxer's behavior changes based on the selected `qcap2_demuxer_type_t`.

### Default Backend (`CreateBackend_default`)
The default backend is a powerful, general-purpose implementation based on **FFmpeg**.

- **Async Engine**: Utilizes `boost::asio` with a thread pool and strands to perform asynchronous I/O and packet processing.
- **FFmpeg Integration**: Uses `AVFormatContext` for demuxing and `AVPacket` for data handling.
- **Bitstream Filtering**: Employs `AVBSFContext` to ensure the output format is compatible with downstream components (e.g., converting MP4 fragments to Annex B for H.264/H.265).
- **Timing & Sync**:
    - **Stream Groups**: Groups related streams and designates a master stream to establish a common time base.
    - **Jitter Buffering**: Implements an internal `AVPacketQueue` to smooth out arrival times.
- **Output**: Buffers packets into `ZzRefCountedBuffer` objects and pushes them into `ZzRefCountedBufferQueue`s.

### Specialized Backends
The SDK provides several other backends for specific hardware or protocols:
- **`pylon` / `usbcam`**: Specialized for industrial and USB cameras.
- **`rtp` / `jsrtsp`**: Optimized for Real-time Transport Protocol and RTSP streams.
- **`fifo`**: Uses named pipes for inter-process communication.
- **`vitis` / `nvt_hdal` / `sc6f0`**: Platform-specific implementations for hardware acceleration.
- **`yuancap`**: Specialized implementation for Yuan capture cards.

## Data Flow
1. **Input**: Data enters via `strURL` or `Push()`.
2. **Backend Processing**: The `Backend` parses the container and extracts packets.
3. **Filtering**: Packets are passed through Bitstream Filters if necessary.
4. **Queueing**: Packets are wrapped in `ZzRefCountedBuffer` and placed in stream-specific `ZzRefCountedBufferQueue`s.
5. **Consumption**: Downstream components (like decoders) `Pop()` the buffers from these queues.
