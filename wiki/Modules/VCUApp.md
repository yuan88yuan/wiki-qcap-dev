# VCUApp Module

The `vcuapp` module consists of application-level utility and test tools for the VCU (Video Coding Unit) hardware.

## Purpose
It provides command-line tools to verify and test VCU hardware encoding and decoding.

## Key Functionality
- **VCU Verification**: Tools for testing encoder and decoder hardware.
- **Advanced Features**: Support for two-pass encoding and ROI (Region of Interest) management.
- **Bitrate Control**: Tools for verifying bitrate control mechanisms.

## Key Files
- `vcuapp/decoder/main.cpp`
- `vcuapp/encoder/main.cpp`
- `TwoPassMngr.cpp`
- `ROIMngr.cpp`
