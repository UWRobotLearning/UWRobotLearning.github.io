---
layout: default
title: BD Spot
parent: Protocols
nav_order: 3
---
**Last Updated:** 2023-08-13

# Using the Boston Dynamics Spot 🐕


## When Not In Use
 TODO: Replace with the up-to-date spot_resting image.


1. **Tablet Location:** Store the tablet on top of the battery charging box. Plug the tablet into the wall charger when not in use.
2. **Battery Location:**
  - Batteries in the **"Full"** Section: 🔋✅ ready
  - Batteries in the **"Empty"** Section: 🔋❌ needs charging
3. **[Charging](https://support.bostondynamics.com/s/article/Spot-Charging-Configurations)**: 
  - If there are batteries left uncharged, please charge them using the Charging Box when around the lab.
  - **DO NOT** leave the batteries charging unattended for longer than 30 minutes.
  - **DO NOT** bend the cable during charging.
4. **Robot Storage:**
  - Keep robot clear of mocap arena.
  - When robot testing is complete, drive Spot back to the area in Allen 014 shown in the image and flip it over so that the battery is easily accessable.
  - **DO NOT** leave the battery inserted when the robot is not operational.
  
## Usage Procedure
1. Insert the Battery. Press and hold the **Power Button** for two seconds. Make sure the **Motor Lockout Button** is pressed for disengaging the hardware motor lock out.
<img src="https://support.bostondynamics.com/servlet/rtaImage?eid=ka04X000000Pn1y&feoid=00N6g00000RYCWq&refid=0EM6g000000QAaR" width="400" height="350">

 > Follow the [Startup Procedure](https://support.bostondynamics.com/s/article/Startup-Procedure) for more detail.

2. Wait for Spot's computers to boot (fans at 100% during startup) and then connect to Spot through its wifi network.
>  TODO: Add log-in stuff location. Log on to Spot using the credentials written in the battery compartment within the belly (do not share these on the internet).

3. Follow the tablet prompts (i.e. "power on motor" and "operate") and test.
> 
6. When testing is complete, walk the robot back over to charging area.
7. [Automatically Roll Spot Over](https://support.bostondynamics.com/s/article/Rolling-Spot-over) (scroll down to bottom of page for instructions)
8. Remove battery from Spot belly.
9. Place partially discharged battery on the left of the Charging Box or begin charging it. Remove from charging before leaving.

## Outdoor Use
- ≥ 2 people must be present when testing.
- Ensure there are no people downhill from the robot at all times (including the operator).
- The operator must be comfortable with the E-stop procedure and the tablet must be configured for E-stop even if Spot is being controlled via the API.
- ❗**Take Video** with phone and/or drone!

## Emergency Stop
Please read the [BD documentation on stopping the robot](https://support.bostondynamics.com/s/article/Stopping-the-robot) for complete info.

E-stop can be run on multiple end-points simultaneously. This means you can start a process in terminal to act as an E-stop (either w/ or w/o gui) as well as use the tablet interface. In my experience so far, the tablet is the best option to use as the primary E-stop.

As long as the tablet is enabled as an E-stop end-point (this means it is actively talking to the robot), this combination of buttons will enable E-stop:

![e-stop tablet](https://support.bostondynamics.com/servlet/rtaImage?eid=ka04X000001LvGq&feoid=00N6g00000RYCWq&refid=0EM4X00000265SU)


## Updating Firmware
[Official BD Downloads Page](https://support.bostondynamics.com/s/downloads)

### Tablet
- Download the App image (.apk) from [Downloads](https://support.bostondynamics.com/s/downloads) page and follow these steps: 
[Tablet Update Procedure](https://support.bostondynamics.com/s/article/Updating-the-Spot-system-software)
### Batteries
### Spot
