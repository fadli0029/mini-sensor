# MiniSensor

## What is this?

MiniSensor is a learning project that implements sensor middleware from scratch. It treats a Raspberry Pi like an embedded sensor (similar to LiDAR or radar in autonomous vehicles) rather than a general-purpose computer. The goal is to understand and demonstrate the low-level programming skills used in robotics/AV infrastructure.

**This is NOT:**
- A production camera streaming service
- A replacement for existing streaming solutions (RTSP, WebRTC, etc.)
- The "best" way to stream video from a Pi

**This IS:**
- A demonstration of real-time systems programming
- An exploration of lock-free data structures
- A simplified version of how actual sensors work in robotics/AVs

## Why Build This?

Simple: **To learn by doing.** Yes, you could install an RTSP server and be streaming in 5 minutes. But then you wouldn't understand:
- How sensors actually communicate in production systems
- Lock-free inter-thread communication patterns
- Custom network protocol design
- Real-time performance optimization
- Memory management in embedded systems

Think of it like building a compiler in a CS course - not because the world needs another compiler, but because it's the best way to understand how they work.

## Architecture Overview

```
Raspberry Pi (Sensor)                    Your Computer (Client)
┌──────────────────┐                    ┌──────────────────┐
│ Camera Module    │                    │ Client SDK       │
│     ↓            │                    │                  │
│ Capture Thread   │                    │ Frame Receiver   │
│     ↓            │      Network       │     ↑            │
│ Lock-Free Buffer │◄──────────────────►│ Frame Assembler  │
│     ↓            │   TCP (commands)   │     ↑            │
│ Network Thread   │   UDP (frames)     │ Display/Process  │
└──────────────────┘                    └──────────────────┘
```

## What you'll see (in-progress)

- **Lock-free Programming**: Single-producer/consumer ring buffers using atomics
- **Network Programming**: Custom TCP/UDP protocols for sensor data
- **Multi-threading**: Thread-safe communication without locks
- **Memory Management**: Pre-allocated pools, zero-copy architecture
- **Real-time Systems**: Deterministic latency, deadline guarantees

## Hardware & Software Requirements

### Raspberry Pi Setup
- Raspberry Pi 4 (4GB RAM minimum)
- Camera Module v2 (Sony IMX219)
- [Ubuntu 22.04 Server for Raspberry Pi (64-bit ARM)](https://cdimage.ubuntu.com/releases/22.04/release/ubuntu-22.04.5-preinstalled-server-arm64+raspi.img.xz)
- Ethernet connection (recommended over WiFi)

### Development Machine
- Ubuntu 22.04 LTS
- C++17 compatible compiler
- CMake 3.17+

## TODO (in-progress)

- [ ] Set up basic project structure and CMake build system
- [ ] Implement TCP command server on Pi
- [ ] Implement TCP command client on laptop
- [ ] Add camera capture interface using libcamera
- [ ] Implement lock-free ring buffer for frame storage
- [ ] Add UDP frame streaming from Pi to client
- [ ] Implement frame packet assembly on client side
- [ ] Add multi-threading for capture and network operations
- [ ] Create performance monitoring and metrics
- [ ] Optimize for low latency (<50ms end-to-end)
- [ ] Add comprehensive error handling and recovery
- [ ] Write unit tests for core components
- [ ] Document API and usage examples

## Learning Resources (in-progress)

This project is inspired by:
- Lock-free programming techniques from "C++ Concurrency in Action"
- Network programming patterns from "Unix Network Programming"
- Writings by Beej

## License

MIT License - see [LICENSE](LICENSE) file for details.
