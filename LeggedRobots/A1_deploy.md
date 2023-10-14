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

- Able to build Yuxiang's repo on
  docker and run it               ✅✅✅

- Able to build Unitree on docker
  and run as well as test the A1   ✅✅✅




## TBD

- Need to send commands through UDP protocol
- Docker run Unitree SDK and test rosnodes
- Need to log data from a1 via UDP protocol
- 

## Issues
- Not responding on v3.5.1
- /usr/bin/ld: cannot find -lunitree_legged_sdk_arm64
collect2: error: ld returned 1 exit status
make[2]: *** [CMakeFiles/robot_interface.dir/build.make:97: robot_interface.cpython-38-aarch64-linux-gnu.so] Error 1
make[1]: *** [CMakeFiles/Makefile2:102: CMakeFiles/robot_interface.dir/all] Error 2
- Not able to build the sole unitree sdk properly on sdk
  without building yuxiang's code.



## Important Links
- [Unitree_sdk_not_working](https://forum.mybotshop.de/t/unitree-a1-unitree-legged-sdk-is-not-working/611)


## Reason

1. Raspberry PI seems to be having the same IP as TX2 (Not currently in the A1). 
   The example codes seem to be setting the controller to HIGH for the A1 which is not possible.
   The code that we tested scales back to 2021 that focuses on Low level controlling.
   
   We used the example position code from the below repo.
   Repository : [Unitree 2020](https://github.com/unitreerobotics/unitree_legged_sdk/blob/918d6c684b3f431416a68370603f470457cf9bae/examples/example_position.cpp)
   

   We were able to run example_position() by manually building it and thus receive data.
   For walking (which was stooping in this case) we were able to build it by following
   Yuxiang's repo and even test it. 
   


