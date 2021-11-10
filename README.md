Automate Home Curtains example project
====================================

A collection of files which define automation rules for curtains **Appliances**.

Automated **Appliance**:

  - curtain.indoor.blackout.Appliance
  - curtain.outdoor.Appliance
  - curtain.outdoor.bedroom.Appliance

## Run Automate Home docker container using this project files

```shell
export AUTOMATE_HOME_CONFIGURATION=`pwd`
export NETWORK_NAME='qnet-static-eth0-a7611e'
export IP='172.31.10.244'

docker run -dit --privileged --name curtains --network $NETWORK_NAME --ip $IP -p 81:81 -p 8181:8181 -v graphite-curtains:/opt/graphite/storage -v redis-curtains:/var/lib/redis -v "$AUTOMATE_HOME_CONFIGURATION:/etc/automate-home" -t automate-home/complete-node:latest
docker exec -it curtains /bin/bash
```

## UI

[GUI example](https://majamassarini.github.io/automate-curtains-example/pages/172.31.10.244/index.html)
