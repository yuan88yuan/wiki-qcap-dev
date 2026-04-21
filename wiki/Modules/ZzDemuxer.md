---
tags: [demuxer, base, av-processing]
last_reviewed: 2026-04-21
related_files:
  - raw/qcap-dev/qcap/src/base/ZzDemuxer.h
  - raw/qcap-dev/qcap/src/base/ZzDemuxer.cpp
---
# ZzDemuxer

`ZzDemuxer` provides a unified interface for demuxing audio and video streams from various sources. It delegates the actual demuxing logic to a specialized `Backend` implementation.

## Purpose
It abstracts the complexity of different input sources (files, network streams, hardware devices) and presents a consistent set of APIs to the rest of the system for retrieving program and stream information.

## Key Functionality
- **Lifecycle Management**: Controls the demuxing process through `Start()`, `Stop()`, `Play()`, and `Update()`.
- **Source Discovery**: Retrieves the number and details of available video sources, audio sources, video encoders, and audio encoders.
- **Program Management**: Manages `ZzProgramInfo` to group related streams into programs.
- **Data Flow**: Provides a `Push()` method for push-sources and manages internal buffering through backends.

## Backends
`ZzDemuxer` supports multiple backends via the `CreateBackend()` method:

- **`default`**: General purpose backend using FFmpeg for URL or push-source demuxing. Supports H.264, H.265, AV1, AAC, and MP2.
- **`pylon`**: Integration with Pylon cameras via the Pylon C API.
- **`usbcam`**: Manages USB cameras and audio devices using `udev`, V4L2, and ALSA.
- **`fifo`**: Optimized FFmpeg-based backend for FIFO-like input.
- **`rtp`**: Handles RTP streams by parsing SDP lines.
- **`jsrtsp`**: Specialized RTSP implementation using the `JSRTSP` library.
- **`vitis`**: Hardware-specific backend for Vitis platforms, managing HDMI RX and hardware broadcasters.
- **`nvt_hdal`**: Hardware-specific backend for NVT HDAL platforms with input format polling.
- **`sc6f0`**: Hardware-specific backend for SC6F0 platforms, leveraging V4L2 media topologies for HDMI/SDI.
- **`experimental`**: Stub backend for testing and development.

## Implementation Details
The core logic is defined in `raw/qcap-dev/qcap/src/base/ZzDemuxer.h` and implemented in `raw/qcap-dev/qcap/src/base/ZzDemuxer.cpp`. Each backend is implemented in its own corresponding file (e.g., `ZzDemuxer_default.cpp`, `ZzDemuxer_vitis.cpp`).
