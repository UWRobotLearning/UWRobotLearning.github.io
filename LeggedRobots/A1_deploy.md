---
layout: default
title: Docker Updates
parent: Updates
nav_order: 1
---

# Unitree on orin

- Installing MuSHR Docker Container  ✅
- Building the MuSHR Docker Stack    ✅
- Adding Unitree SDK to Docker Stack ✅
- Able to Ping A1 via orin           ✅
- Able to build unitree sdk on stack ✅

- Building Unitree v3.5.1            ✅
    1. Dependency issue was libboost ✅
    2. LCM not needed to be resolved ✅
- Quad walks after running Yuxiang's
  repo code                       ✅✅✅



## Interesting developments
- Able to get "some" data from 
  unitree after sshing into it via 
  wifi

## TBD

- Need to send commands through UDP protocol
- Docker run Unitree SDK and test rosnodes
- Need to log data from a1 via UDP protocol
- Need another unitree v? 2.8.0, 3.2.0

## Issues
- Not responding on v3.5.1
- /usr/bin/ld: cannot find -lunitree_legged_sdk_arm64
collect2: error: ld returned 1 exit status
make[2]: *** [CMakeFiles/robot_interface.dir/build.make:97: robot_interface.cpython-38-aarch64-linux-gnu.so] Error 1
make[1]: *** [CMakeFiles/Makefile2:102: CMakeFiles/robot_interface.dir/all] Error 2



## Important Links
- [Unitree_sdk_not_working](https://forum.mybotshop.de/t/unitree-a1-unitree-legged-sdk-is-not-working/611)

