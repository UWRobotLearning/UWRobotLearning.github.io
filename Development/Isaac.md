In this article, note that `~/WORKING_DIR/` refers to any directory that will contain the cloned repo.

TODO: insert the image explaining differences.

when developing the simulator physics engine, Nvidia wanted to "preview" it early and they exposed only the rigibody physics components via isaacgym api which is any code you see calling "gymapi" or "gymtorch"
## Isaac Gym

See Virtual Environments section

Download [IsaacGym Preview 4](https://developer.nvidia.com/isaac-gym) to `~/WORKING_DIR/`
>**Note:** old docs can be found at: `~/WORKING_DIR/isaacgym/docs/index.html

<details markdown="block">
<summary> Install Commands (expand) </summary>
```bash
cd ~/WORKING_DIR/isaacgym/python 
conda create -n environment_name_goes_here python==3.8
conda activate environment_name_goes_here
pip install -e .

#test to make sure isaacgym is running correctly
cd ~/WORKING_DIR/isaacgym/python/examples
python 1080_balls_of_solitude.py
```
</details>


leggedgym
[isaacgymenvs](https://github.com/NVIDIA-Omniverse/IsaacGymEnvs)


## Isaac-Sim
- documentation
- requires NVidia RTX GPU

default api (omni.isaac.core)
- Robot
- Franka
default gym api (omni.isaac.gym)

[orbit](https://github.com/NVIDIA-Omniverse/Orbit)
[omniisaacgymenvs](https://github.com/NVIDIA-Omniverse/OmniIsaacGymEnvs)
