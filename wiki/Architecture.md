# Architecture

The QCAP SDK is a modular C/C++ library for video and audio capture, processing, encoding, and streaming.

## High-Level Design
The SDK follows a pipeline-based architecture consisting of several key components:
- **Capture Sources**: Video and audio capture from cameras, sound cards, and network streams.
- **Processing Filters**: Deinterlacing, color space conversion, and audio resampling.
- **Encoders**: H.264, H.265, and AAC encoding.
- **Muxers**: Containerization into MP4 or MPEG-TS.
- **Output Sinks**: Saving to files, network streaming, or display.

## API Layers
The SDK exposes two distinct APIs to cater to different use cases:
1. **Traditional C API (`qcap.h`)**: A procedural API providing direct control over the pipeline.
2. **Modern C API (`qcap2.h`)**: An object-oriented C API allowing modular construction of custom pipelines.

## Platform Support
The SDK is designed for high portability across various Linux distributions and embedded platforms (e.g., HiSilicon, NVIDIA L4T, Novatek, etc.), utilizing platform-specific implementations for hardware acceleration.

## Directory Structure
- `/raw/qcap-dev/qcap/src/`: Core implementation.
- `/raw/qcap-dev/qcap/include/`: Public API headers.
- `/raw/qcap-dev/qcap/3rdparty/`: Pre-built platform-specific libraries.
- `/raw/qcap-dev/qcap/build-qcap/`: Build system configurations.
