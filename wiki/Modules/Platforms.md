# Platforms

The QCAP SDK provides extensive support for various hardware and software platforms through specialized implementations.

## Platform Implementations
Platform-specific code is located in `raw/qcap-dev/qcap/src/` and is generally named after the platform:

### HiSilicon
- `hi3519a/`
- `hi3531a/`
- `hi3531a400/`
- `hi3531a510/`
- `hi3531d/`
- `hi3559a/`
- `hi3559a210/`
- `hisiv_base/` (Common base for HiSilicon platforms)

### NVIDIA / Jetson (L4T)
- `l4t3250/`
- `l4t3510/`

### Other Platforms
- `sc6e0/`, `sc6f0/`, `sc6g0/`, `sc6n0/`, `sc6t0/`
- `novatek/` (likely mapped to certain `sc6` or others)
- `linux_base/` (Common base for Linux platforms)

## Platform-Specific Configuration
Build configurations for these platforms are found in `raw/qcap-dev/qcap/build-qcap/*.mk`.
