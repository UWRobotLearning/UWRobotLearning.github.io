---
layout: default
title: Set Up Perception Pipeline for A1
parent: Tutorials
nav_order: 2 
mathjax: true
---
**Last Updated:** 2021-07-20

# Setting Up Perception Pipeline for A1
This tutorial goes through steps to set up the perception pipeline for the A1 quadruped robot, which includes installing drivers for the RealSense D435i camera, installing `pytorch` and `torchvision` specifically for the TX2 platform.

## Connecting to the Robot
By default, the A1 robot has a built-in wifi HotSpot named `UnitreeRoboticsA1-XXX`, where `XXX` is the robot serial number. To access the onboard TX2, connect to the wifi hotspot (default password is `00000000`). Then you can `ssh` into the robot by running:

`ssh unitree@192.168.123.12`

with password `123`.

## Setup Internet Access
It would be beneficial to have internet access in the TX2 during the setup process. You can either connect a ethernet cable to the robot and make sure that the IP address is correctly setup, or use a usb wifi adapter. 

If using a usb wifi adapter, you need to enable it by running:

`sudo /etc/init.d/network-manager start`

and connect to wifi using 

`sudo nmtui`

Note that this will override the robot's default wifi setting, so the Unitree hotspot is no longer accessible. You have to connect to the robot via ethernet cable.

## Setup Intel Realsense D435i
In my experience, the only way I found working is to build the SDK by following the script [here](https://github.com/jetsonhacks/installRealSenseSDK/blob/master/buildLibrealsense.sh). It will take ~30 minute for the entire compilation to complete. Once done, test the device connection by running `rs-enumerate-devices`. If you connect the TX2 to the monitor, you can also check video footage by running `realsense-viewer`.

To setup python API access, the simplest way I have found is to directly run the following command:

`pip install pyrealsense2-aarch64`

Here's a simple script to test the image interface:
```python
"""Example for real-time semantic segmentation using realsense camera."""
from absl import app
from absl import flags
from absl import logging

import cv2
from datetime import datetime
import numpy as np
import os
import pyrealsense2 as rs
import torch
import yaml

flags.DEFINE_string('output_dir', 'logs', 'Frame output dir.')
FLAGS = flags.FLAGS


def main(_):
  if not os.path.exists(FLAGS.output_dir):
    os.makedirs(FLAGS.output_dir)
  pipeline = rs.pipeline()
  config = rs.config()
  config.enable_stream(rs.stream.color, 1280, 720, rs.format.bgr8, 10)
  profile = pipeline.start(config)
  try:
    while True:
      frames = pipeline.wait_for_frames()
      color_frame = frames.get_color_frame()
      color_image = np.array(color_frame.get_data())
      filename = "img_{}.png".format(
          datetime.now().strftime('%Y_%m_%d_%H_%M_%S_%f'))
      cv2.imwrite(os.path.join(FLAGS.output_dir, filename), color_image)
      logging.info("Image captured.")
  finally:
    pipeline.stop()


if __name__ == "__main__":
  app.run(main)
```

## Setup `pytorch` 

TX2 has specific hardware / cuda versions that standard `pip`-installed wheels do not support. The official [thread](https://forums.developer.nvidia.com/t/pytorch-for-jetson-version-1-9-0-now-available/72048) contains a set of pre-built wheels for pytorch and jetson hardware.

For my A1 robot, the cuda version installed only supports `pytorch` up to `1.4.0`. To install the specific version, run:

`wget https://nvidia.box.com/shared/static/ncgzus5o23uck9i5oth2n8n06k340l6k.whl -O torch-1.4.0-cp36-cp36m-linux_aarch64.whl`

and install it by running:

`pip3 install Cython numpy torch-1.4.0-cp36-cp36m-linux_aarch64.whl`

Note: do not install `numpy` version `1.19.5` yet as it is not supported.

Once everything working, you should be able to `import torch` in python, and `torch.cuda.is_available()` should return `True`.

## Setup `torchvision`
For pytorch `1.4.0`, the corresponding `torchvision` version is `0.5.0`. However, the `pip`-hosted pre-built wheel for `0.5.0` does not support aarch64 architecture yet. Fortunately, [this site](https://github.com/KumaTea/pytorch-aarch64/blob/main/README.md) kindly hosts some pre-built wheels for `torchvision`, including the `0.5.0` version. Download the built wheels by running:

`wget https://github.com/KumaTea/pytorch-aarch64/releases/download/v1.4.1/torchvision-0.5.0-cp36-cp36m-linux_aarch64.whl`

and install it by running:

`pip install torchvision-0.5.0-cp36-cp36m-linux_aarch64.whl`

If all are working properly, you should be good to go!
