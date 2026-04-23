---
tags: [qcap2, oo-api, modules]
last_reviewed: 2026-04-21
related_files:
  - raw/qcap-dev/qcap/include/qcap2.h
  - raw/qcap-dev/qcap/src/qcap2/
---
# QCap2 OO API Modules

The `qcap2` API provides a modern object-oriented interface for the QCAP SDK. It is implemented primarily within the `qcap/src/qcap2` directory.

## A/V Core Components
These modules handle the primary flow of audio and video data.
- **Sources**: `qcap2_video_source_t` (`ZzVideoSource`), `qcap2_audio_source_t` (`ZzAudioSource`) - Capture data from various inputs.
- **Sinks**: `qcap2_video_sink_t` (`ZzVideoSink`), `qcap2_audio_sink_t` (`ZzAudioSink`) - Output data to various destinations.
- **Codecs**: 
    - `qcap2_video_encoder_t` (`ZzVideoEncoder2`), `qcap2_video_decoder_t` (`ZzVideoDecoder2`)
    - `qcap2_audio_encoder_t` (`ZzAudioEncoder2`), `qcap2_audio_decoder_t` (`ZzAudioDecoder2`)
- **Processing**: 
    - `qcap2_video_scaler_t` (`ZzVideoScaler`) - Handles scaling and format conversion.
    - `qcap2_audio_resampler_t` (`ZzAudioResampler2`) - Handles audio sample rate conversion.

## Muxing & Demuxing
Modules for combining or separating multiple A/V streams.
- **Demuxing**: 
    - `qcap2_demuxer_t` (`ZzDemuxer`) - Extracts streams from a container.
    - `qcap2_program_info_t` (`ZzProgramInfo`) - Describes a program within a demuxed stream.
- **Muxing**: `qcap2_muxer_t` (`ZzMuxer`) - Combines streams into a container.
- **Filtering**: `qcap2_bitstream_filter_t` (`ZzBitstreamFilter2`) - Modifies compressed bitstreams.

## Buffer & Memory Management
Provides high-performance memory handling for A/V frames and packets.
- **Reference Counting**: `qcap2_rcbuffer_t` (`ZzRefCountedBuffer2`) - Core buffer type with reference counting.
- **Queuing**: `qcap2_rcbuffer_queue_t` (`ZzRefCountedBufferQueue`) - Thread-safe buffer queues.
- **Pooling**: 
    - `qcap2_frame_pool_t` (`ZzFramePool`) - Recycles video/audio frames.
    - `qcap2_packet_pool_t` (`ZzPacketPool`) - Recycles A/V packets.

## Synchronization & Events
Low-level primitives for multi-threaded coordination.
- **Events**: 
    - `qcap2_event_t` (`ZzEvent2`) - Event signal/wait primitive.
    - `qcap2_event_handlers_t` (`ZzEventHandlers`) - Manages event callbacks.
- **Timing**: `qcap2_timer_t` (`ZzTimer`) - Precision timing and timeouts.
- **Locks**: 
    - `qcap2_benaphore_lock_t` (`ZzBenaphoreLock`) - Hybrid spin/mutex lock.
    - `qcap2_block_lock_t` (`ZzBlockLock`) - Blocking synchronization.

## Device & System Management
Handles hardware discovery and system resources.
- **Device**: 
    - `qcap2_qdev_t` (`ZzQdev`) - Represents a physical or virtual device.
    - `qcap2_qdev_enum_t` (`ZzQdevEnum`) - Enumerates available devices.
    - `qcap2_qdev_info_t` (`ZzQdevInfo`) - Contains device metadata.
- **Clocking**: `qcap2_clock_source_t` (`ZzClockSource`) - Provides a synchronized system clock.

## Formats & Properties
Data structures describing the characteristics of A/V streams.
- **Formats**: `qcap2_input_format_t`, `qcap2_video_format_t`, `qcap2_audio_format_t`
- **Properties**: 
    - `qcap2_video_encoder_property_t` - Static encoding settings.
    - `qcap2_audio_encoder_property_t` - Static audio encoding settings.
    - `qcap2_video_encoder_dynamic_property_t` - Settings that can change during runtime.

## Graphics & UI
Tools for visual output and overlay composition.
- **Windows**: `qcap2_window_t` (`ZzWindow`) - Manages OS-level display windows.
- **Graphics**: 
    - `qcap2_graphics_t` (`ZzGraphics`) - Core 2D graphics operations.
    - `qcap2_font_atlas_t` (`ZzFontAtlas`) - Manages font glyphs.
- **Composition**: 
    - `qcap2_video_blender_t` (`ZzVideoBlender`) - Mixes multiple video layers.
    - `qcap2_video_matte_t` (`ZzVideoMatte`) - Handles alpha masking and matting.

## Utilities
Miscellaneous helper modules.
- **Binding**: `qcap2_binder_t` (`ZzBinder`) - Connects sources to sinks (e.g., source to scaler).
- **Information**: `qcap2_media_info_t` (`ZzMediaInfo`) - Aggregated metadata for a media source.
