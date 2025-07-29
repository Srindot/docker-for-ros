# Docker File for ROS2 Humble

This repositary provides a Dockerized development environment for :

1. **ROS2(Humble)**
2. **ROS2(Humble), Gazebo(Ignition) and PX4** integration with **QGroundControl**


## **Usage**


Make sure you have the following dependencies installed:
- Docker
- xhost


### Clone the Repository

For setting up the docker environment clone this repository:

```bash
git clone https://github.com/Srindot/ROS-docker-setup.git
```

To build the Docker Image, navigate to one of the dockerfiles in the project directory:

For example like below

```bash
cd ROS-docker-setup/ros2-humble
```

Build the docker file with the following command.

```bash
docker build -t image_name:tag .
```

After building the docker image, a container can be created with the name as `image_name` using the built image by the following command

```bash
xhost +local:docker && docker run -it \
  --name contianer_name \
 --privileged \
  -e DISPLAY=$DISPLAY \
  -e PULSE_SERVER=unix:/run/user/$(id -u)/pulse/native \
  --volume=/run/user/$(id -u)/pulse/native:/run/user/$(id -u)/pulse/native \
  --device /dev/snd \
  --group-add audio \
  --net=host \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume /home/$(whoami)/.Xauthority:/root/.Xauthority:ro \
  image_name:tag

```

To exit the container

```bash
exit
```

To stop the container

```bash
docker stop contianer_name
```

To start the container again

```bash
docker start contianer_name 
```

To enter to the bash

```bash
docker exec -it contianer_name /bin/bash
```

To remove the container

```bash
rm -f contianer_name
```


## Troubleshooting

Ensure your host system supports GUI applications (e.g., X11) for GUI tools to display correctly.

If you face any troubles, please open an issue in GitHub.
