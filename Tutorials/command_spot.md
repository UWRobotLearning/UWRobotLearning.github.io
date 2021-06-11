---
layout: default
title: Commanding Spot
parent: Tutorials
nav_order: 2
mathjax: true
---
**Last Updated:** 2021-06-11

🚧 Work In Progress
{: .label .label-yellow}

![Arm](https://d33wubrfki0l68.cloudfront.net/d7fde05575f5064aa5f6b57b0c9424d2e7da5b79/f9951/_images/arm-diagrams-02.png)

# Sending Commands to Boston Dynamics Spot

## Prerequisites

1. Follow the BD [Quickstart Tutorial](https://dev.bostondynamics.com/docs/python/quickstart) first.
- Possible issues:
   - Issue: "InternalServerError"
   - Fix: Restart robot
   - Issue: "CommandFailedError('Stand (ID X) no longer processing...)"
   - Fix: Physically orient the robot on its legs.

## Summary of Quickstart

**1. SDK Init:**
```python
import bosdyn.client
sdk = bosdyn.client.create_standard_sdk('rosario')
robot = sdk.create_robot('192.168.80.3')
```

**2. Authentication:**
```python
robot.authenticate('user', 'password')
```

**3. Clear E-stop:**
```python
estop_keep_alive = bosdyn.client.estop.EstopKeepAlive(estop_endpoint)
print(estop_client.get_status())
```

**4. Acquire Lease:**
```python
lease_client = robot.ensure_client('lease')
lease_client.take() # forcefully takes lease (equiv to using 'hijack' in the teleop interface)
lease_keep_alive = bosdyn.client.lease.LeaseKeepAlive(lease_client)
print(lease_client.list_leases())
```

**5. Power On:**
```python
robot.power_on(timeout_sec=20)
print(robot.is_powered_on())
```

**6. Time Sync:**
```python
robot.time_sync.wait_for_sync()
```

**7. Stand Up:**
```python
from bosdyn.client.robot_command import RobotCommandClient, blocking_stand
command_client = robot.ensure_client(RobotCommandClient.default_service_name)
blocking_stand(command_client, timeout_sec=10
```

**8. Power Off:**
```python
robot.power_off(cut_immediately=False
```

## References

[Official Spot SDK](https://dev.bostondynamics.com/)
