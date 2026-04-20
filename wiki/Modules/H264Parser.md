# H264Parser Module

The `h264parser` module is a dedicated low-level H.264 bitstream parser.

## Purpose
It provides specialized parsing for H.264 encoded streams.

## Key Functionality
- **NAL Unit Parsing**: Parsing of Network Abstraction Layer units.
- **AVCC Support**: Parsing of AVCC headers.
- **SEI Parsing**: Extraction of Supplemental Enhancement Information messages.

## Key Files
- `h264_stream.cpp`
- `h264_avcc.cpp`
- `h264_sei.cpp`
