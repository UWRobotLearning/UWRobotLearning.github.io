---
layout: default
title: Setting up ROS for A1 
parent: Tutorials
nav_order: 2 
mathjax: true
---

**Last Updated: 2021-10-04**

# Setting up ROS for A1
This tutorial goes through steps to set up the [Robot Operating System (ROS)](https://www.ros.org/) pipeline for the A1 quadruped robot. 
In our case, we use a Mac-Mini with M1 processor (running Ubuntu 20.04 Virtual Machine using the Parallels) for high-frequency model predictive control,
and the on-board Nvidia Jetson TX2 (running Ubuntu 18.04) for perception and other tasks.
Many parts tutorial should be helpful for other uses of ROS on the A1 quadruped platform.

## Why ROS?
While ROS is not necessarily required for the operation of A1, we choose ROS for a number of benefits:

1. Distributed, parallel computation with easy inter-process message passing.

Note that different components of the A1's control pipeline are inherently asynchronous (e.g. camera perception process might run at a significantly lower frequency compared to the control process) and distributed (e.g. we run perception on TX2 to utilize its GPU, and run control on M1 to utilize its CPU). Moreover, components of the pipeline should be interchangable (e.g. one should easily replace an automatic SLAM-based controller with a manual controller). This calls for easy inter-process and inter-machine message passing, which is one of the core features of ROS.

2. Automated logging for easy debugging.

Manually implements the logging of every component in the control pipeline can be tedious. Instead, ROS can automatically log all topics via [rosbag](http://wiki.ros.org/rosbag), and most of the screen logs are also automatically saved, which significantly simplifies debugging.
Another 

3. Easy integration with mobile devices for outdoor testing.

It can be challenging to carry a laptop when testing the robot outdoors. Instead, it would be much easier if one could view the robot's state on a phone. Thankfully, the [ROS-Mobile](https://github.com/ROS-Mobile/ROS-Mobile-Android) project allows you to do exactly this on Android. While it doesn't support all message types yet, it's already supporting image and text, and works nicely with ROS-Noetic.

Also, keep in mind that, despite its benefits, ROS1 is **not** feasible for high-frequency, real-time computation. The core message passing is based on [xmlrpc](http://xmlrpc.com/), which is optimized more for compatiability than for performance. Therefore, I do not use ROS for low-level model predictive control.

## What is covered in this tutorial?
1. Installing ROS Noetic on Ubuntu 18.04 in TX2.
2. Network setup for TX2 and M1.
3. Make ROS processes run at boot time.
4. Using the ROS-Mobile App to simplify outdoor testing.

## Installing ROS Noetic on Ubuntu 18.04 in TX2
As Noetic is the first ROS version that directly supports Python3, it is much more friendly for modern Python scripts utilizing latest machine learning libraries. Unfortunately, Jetson TX2 currently only supports Ubuntu 18.04, while ROS Noetic only supports Ubuntu 20.04 and above. Fortunately, it is possible to compile ROS Noetic _from source_ in Ubuntu 18.04. The official [guide](http://wiki.ros.org/noetic/Installation/Source) to compile from source does **not** work for my TX2 due to some compatiability issues. Another option is to use the official Docker [scripts](https://github.com/dusty-nv/jetson-containers), but I had a difficult time configuring the network within Docker.

In the end, I was able to compile ROS Noetic without docker by mostly executing the docker [script](https://github.com/dusty-nv/jetson-containers/blob/master/Dockerfile.ros.noetic) directly to the shell. I also changed the `ROS_PKG` environment variable in line 8 from `ros_base` to `desktop` as that compiles a lot more useful packages than the barebone version (`desktop-full` failed for some packages iirc). It does significantly increase the compile time though.

Also, follow this [guide](https://uwrobotlearning.github.io/Tutorials/a1_perception_setup.html) to install pytorch, torchvision and camera drivers on the TX2.

## Network setup for TX2 and M1
### TX2: ROSMaster and Perception
I choose to run `rosmaster` and most of the perception pipelines on TX2, and run control-related ros nodes on M1. Since TX2 is connected to both Ethernet (M1) and Wifi (external devices), running `rosmaster` on TX2 allows most messages to be broadcast to both networks. Since the bridging between Wifi and Ethernet is already set on TX2, we only need to configure the environment variables by adding the following to `~/.bashrc`:
```
export ROS_MASTER_URI=http://192.168.123.12:11311
export ROS_IP=192.168.123.12
```
After that, the ROSMASTER should be visible to devices connected via both ethernet and wifi.

### M1: Settings inside the Parallels virtual machine
Running ROS nodes inside the VM and having it connecting to the external TX2 can be tricky. Parallels provides two [ways](https://kb.parallels.com/4948) to configure the networking of virtual machines, where `Shared` encapsulates the VM inside Mac and only shares the internet, and `Bridged` exposes the VM directly to Mac's network as an individual machine. While `Bridged` sounds like the correct choice here, I found it particularly difficult and flaky to work with. Specifically, the first boot of the VM after starting Mac does not connect to the robot's network, and I had to manually re-boot for the bridging to work. Moreover, the bridge is broken from time to time, and when it breaks, you don't even have a way to `ssh` into the VM. Parallels state that they are `no longer responsible for any network connectivity issues` in the bridged mode`.

While Parallels does not share the details of how `Shared` networking operates, I have successfully configured it so that ROS installed in the VM can talk to TX2 directly. Here are the steps I followed:
1. Manually set Mac-Mini's ip to be within the same subnet of the TX2 as `192.168.123.xx`, so that you can ping/ssh into TX2 from your Mac-Mini. 
2. Log in to VM, and check that you can ping TX2's IP (`192.168.123.12`) and ssh into it (`ssh unitree@192.168.123.12`) directly from **inside** the VM. This should work automatically as long as your previous step is configured correctly. Also, your `ssh` activity to TX2 should be recorded as coming from the Mac-Mini's ip.
3. Add the following environment variables to `~/.bashrc` **inside** the VM:
```
export ROS_MASTER_URI=http://192.168.123.12:11311
```
and check that running `rostopic list` can identify TX2's ROS topics.
4. Publish some messages on TX2, and check whether you can receive them on M1 by running `rostopic echo`. If you can see the topic name, but cannot see the actual messages being published, try adding TX2's hostname to the VM's `/etc/hosts` file, or see [this post](https://answers.ros.org/question/90536/ros-remote-master-can-see-topics-but-no-data/) for more helps in trouble-shooting.

## Make ROS processes run at boot time
Since the robot can suffer from unexpected conditions and stop/reboot randomly esp. during outdoor operation, it can be painful to re-connect to the robot every time and manually start the ROS processes. There are several ways to make scripts run at start-up in Ubuntu, including [`init.d`](https://en.wikipedia.org/wiki/Init), [`systemd`](https://en.wikipedia.org/wiki/Systemd), [`cron` @reboot](https://phoenixnap.com/kb/crontab-reboot) and [`autostart`](https://arcolinux.com/how-to-autostart-any-application-on-any-linux-desktop/). They operate at different levels. At the abstract level, `init.d` runs at OS bootup. `systemd` runs as a service when OS is running. `cron` is a `systemd` service that allows more flexible scheduling. `autostart` is Ubuntu-specific that's tied to Gnome.

Since ROS requires networking, putting it in `init.d` requires careful ordering and can be tricky. `autostart` and `cron` don't have good support on defining custom environment variables or sourcing other bash scripts, which is required for ROS. Therefore, I have found `systemd` to be the easiest way to configure this.

To add a new script that runs at start-up, first create a new service in `/etc/systemd/system/[service name].service` with the following content:
```
[Unit]
Description=YOUR DESCRIPTION HERE

[Service]
ExecStart=ABSOLUTE PATH TO YOUR BASH SCRIPT
User=YOUR USER NAME, OR LEAVE EMPTY AND IT WILL BE RUN UNDER ROOT

[Install]
WantedBy=multi-user.target
```

Then reload the system services by running:

```systemctl daemon-reload```

and run the system services by running:

```sudo systemctl [enable/start/restart] [service name]```

You can also check the logs at `/var/log/syslog` to debug any errors.

I created the service on both TX2 and M1 so that both the master and remote processes can start at boot time. 
Hint: by default, `roslaunch` throws an error when it cannot detect `rosmaster` and `rosmaster` is on a remote machine. Use `--wait` flag in `roslaunch` would make it wait till the remote `rosmaster` has started.

## Using the ROS-Mobile App to simplify outdoor testing.
The app is available both on [GitHub](https://github.com/ROS-Mobile/ROS-Mobile-Android) and [Play Store](https://play.google.com/store/apps/details?id=com.schneewittchen.rosandroid). It has a few glitches but is mostly working fine for me. Simply connect to the robot wifi and specify the ROS's master address (`192.168.123.12:11311`) and conect to it. You should then be able to add different widgets in the details tab and visualize your topics on your Android phone!
