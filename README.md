automate-home curtains example project
======================================

An example project for the [automate-home project](https://github.com/majamassarini/automate-home).

A collection of files which define automation rules for 3 different curtains **Appliances**.

  - [curtain.indoor.blackout.Appliance](https://automate-home.readthedocs.io/en/latest/appliances.html#curtain-indoor-blackout-appliance)
  - [curtain.outdoor.Appliance](https://automate-home.readthedocs.io/en/latest/appliances.html#curtain-outdoor-appliance)
  - [curtain.outdoor.bedroom.Appliance](https://automate-home.readthedocs.io/en/latest/appliances.html#curtain-outdoor-bedroom-appliance)

Every *Appliance* automates a device, through a *Performer*. 
The automated devices are 3 equals **KNX** actuators for blind/shutters which understand just an *opened* and a *closed command*.

To automate the curtains 2 sensors are used:

  - [sensor.luxmeter.Appliance](https://automate-home.readthedocs.io/en/latest/appliances.html#sensor-luxmeter-appliance); data come from a **KNX** sensor.
  - [sensor.anemometer.Appliance](https://automate-home.readthedocs.io/en/latest/appliances.html#sensor-anemometer-appliance); data come from an **Home Assistant** virtual sensor listening a weewx supported device.

## Project notes

  1. The *indoor blackout curtain* is not completely automated, the system is just able to open it and not to close it.
     
     This is because my window does not have a sensor telling the system if it is opened; if the indoor curtain goes 
     down when the window is opened it is a huge problem.
 
  2. The *outdoor curtain* has the *sun hit* event disabled, the event which tells the curtain if the sun is hitting its
     window. 
     
     This is because I want more light in the room in the winter.

## Run automate-home docker container using this project files

```shell
export AUTOMATE_HOME_CONFIGURATION=`pwd`
export NETWORK_NAME='qnet-static-eth0-a7611e'
export IP='172.31.10.244'

docker run -dit --privileged --name curtains --network $NETWORK_NAME --ip $IP -p 81:81 -p 8181:8181 -v graphite-curtains:/opt/graphite/storage -v redis-curtains:/var/lib/redis -v "$AUTOMATE_HOME_CONFIGURATION:/etc/automate-home" -t majamassarini/automate-home:latest
docker exec -it curtains /bin/bash
```

## UI

[GUI example](https://majamassarini.github.io/automate-curtains-example/pages/172.31.10.244/index.html)
