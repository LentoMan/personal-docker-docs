# Technical Overview
This section describes how the personal docker series achieves offline mode. It also describes how and where data is stored using bind mounts.

## Offline mode

In offline mode, the webui container is only allowed to communicate with other containers inside a docker internal network. An additional "tunnel" container is created which has access to both the external and internal docker networks. The tunnel simply listens to the port where the webui would normally reside on the external network and forwards the traffic to the webui container on the internal network.

When running in offline mode, a communication attempt with the outside world is performed during startup. The webui container tries to ping the Google DNS server at 8.8.8.8, which should never succeed in this mode. If it does succeed, the webui container simply aborts the launch.

### Bind mounts

The external webui directory is mounted into the container with a bind mount, this means you can easily access and modify all source code and data from outside the container. 

To make sure files and directories created inside the container gets the proper external user id, the id of your external user is set in the `user.env` file as the `setup.sh` script runs. Your external user id is then read from the `user.env` during container startup and set for the `ubuntu` user inside the container.

The users home directory is mounted into the `<webui>/cache/home` of the repo and tmpdir is mounted into `<webui>/tmp` of the repo.
