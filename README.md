# MIDrone

A custom-built quadcopter flight controller running on a Raspberry Pi Pico — a personal build inspired by and based on [Tim Hanewich's Scout Flight Controller](https://timhanewich.medium.com/my-greatest-engineering-accomplishment-the-scout-flight-controller-d8937fb45b24).

## Overview

MIDrone is a from-scratch quadcopter project: instead of using an off-the-shelf flight controller (e.g. ArduPilot/Betaflight), it runs a custom **MicroPython** flight control loop directly on a Raspberry Pi Pico (RP2040). The control software reads gyroscope data over I2C, compares it against pilot input received via an RC receiver, and drives four ESCs through PID-controlled PWM signals — all at a 250 Hz update rate.

The hardware selection differs from the original Scout build in a few deliberate ways (gentler motors sized for the actual build weight, a separate power distribution board instead of a frame with an integrated one, etc.) — see [Hardware](#hardware) below.

## Credits

This project would not exist without **Tim Hanewich's** open documentation:

- Article series: [My Greatest Engineering Accomplishment: The Scout Flight Controller](https://timhanewich.medium.com/my-greatest-engineering-accomplishment-the-scout-flight-controller-d8937fb45b24)
- Successor project: [Centauri](https://github.com/TimHanewich/centauri) / [Full-Stack Flight](https://medium.com/@timhanewich/full-stack-flight-building-a-quadcopter-ecosystem-from-scratch-18d43386bb6d)

## Hardware

| Component | Choice |
|---|---|
| Microcontroller | Raspberry Pi Pico (RP2040) |
| Frame | F450 (450mm), bare frame + separate PDB |
| Motors | EMAX MT2213 935KV (2x CW, 2x CCW) |
| ESCs | 30A, BEC-equipped |
| Propellers | 10x4.5" |
| Battery | 4S LiPo, 3300 mAh, 50C |
| IMU | MPU-6050 (GY-521 breakout) |
| RC | FlySky FS-i6 transmitter + FS-iA6B receiver (ibus) |

## Software

- **Language:** MicroPython
- **Control loop:** 250 Hz, rate-mode PID (roll / pitch / yaw), procedural (not OOP) for performance
- **Sensor:** MPU-6050 over I2C, gyro-bias calibrated at boot
- **Pilot input:** FlySky ibus protocol over UART
- **Output:** PWM to 4 ESCs
- **Safety interlocks:** refuses to arm if flight-mode switch is already on at boot; refuses to arm if throttle is non-zero when switching into flight mode

## Status

🔧 **Parts sourcing complete — build not yet started.**

- [x] Researched and selected all hardware
- [x] Parts ordered
- [ ] Assembly
- [ ] Flight controller firmware adapted to this build's PID/motor parameters
- [ ] Ground testing (props off)
- [ ] Tethered first flight
- [ ] Free flight

This README will be updated as the build progresses.

## License

This project is licensed under the [MIT License](LICENSE).

Flight control logic is derived from Tim Hanewich's Scout project, also MIT-licensed — see the [upstream repository](https://github.com/TimHanewich/scout) for the original license terms.
