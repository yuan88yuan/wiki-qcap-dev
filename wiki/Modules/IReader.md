# IReader Module

The `ireader` module is a comprehensive library for reading and parsing a wide variety of media protocols and containers.

## Purpose
It implements demuxers and parsers for various media formats and protocols.

## Key Functionality
- **Container Support**: Parsers for MP4/MOV, MKV, MPEG-TS, and FLV.
- **Protocol Support**: Implementation of RTSP, RTMP, HTTP, SIP, and RTP/RTCP.
- **Audio Decoding**: Integration of audio decoders.

## Key Files
- `librtsp/rtsp-client.c`
- `librtmp/rtmp-client.c`
- `libmov/mov-reader.c`
- `libmpeg/mpeg-ts-dec.c`
- `avcodec/audio-decoder.c`
