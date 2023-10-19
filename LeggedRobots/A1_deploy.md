---
layout: default
title: Docker Updates
parent: Updates
nav_order: 1
---

# Steps:
- cd ~/temp/fast_and_efficient
- source .env/bin/activate  (activating python3.8)
- python -m src.robots.a1_robot_exercise_example --use_real_robot=True


# Redundant libs in requirements.txt in fast_and_efficient
- tensorflow
- pybullet
- ml_collections


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


## Issues
- Not responding on v3.5.1
- /usr/bin/ld: cannot find -lunitree_legged_sdk_arm64
collect2: error: ld returned 1 exit status
make[2]: *** [CMakeFiles/robot_interface.dir/build.make:97: robot_interface.cpython-38-aarch64-linux-gnu.so] Error 1
make[1]: *** [CMakeFiles/Makefile2:102: CMakeFiles/robot_interface.dir/all] Error 2
- Not able to build the sole unitree sdk properly on sdk
  without building yuxiang's code.

- Not able to run "python -m src.robots.a1_robot_exercise_example --use_real_robot=True" without installing the requirements.



## Resolving unitree sdk build issue

1. Raspberry PI seems to be having the same IP as TX2 (Not currently in the A1). 

   IP for the unitree quadruped is 192.168.123.X

   Sport mode uses a high level controller (need to confirm this properly)
   If sport mode, it communicates with a Tx2, X = 161 
   Basic mode uses low level controller (need to confirm this properly)
   If basic mode it communicates directly with a embedded board (not-ssh'able), X = 10

   The `example_walk` sets the control level to HIGH for the A1 which is meant to interface with the default-from-factory TX2 in 'SPORT MODE'.
   Because the TX2 was removed on the A1 named "Ghost", commands via SPORT MODE won't work.
   What makes this even more confusing is that there is a raspberry Pi installed as a replacement for the TX2 on "Ghost" which has the same IP (X=161) set.
   We were able to build and run a different `example_position` code which communicates with the Basic mode and works. We obtained this example from an earlier version of the codebase (note there are changes to API since then, such as the UDP constructors).
   
   We used the example position code from the below repo.
   Repository : [Unitree 2020](https://github.com/unitreerobotics/unitree_legged_sdk/blob/918d6c684b3f431416a68370603f470457cf9bae/examples/example_position.cpp)
   

   We were able to run example_position() by manually building it and thus receive data.
   Python scripts which use Pybind bindings to communciate at the low level API still work as expected.



   


