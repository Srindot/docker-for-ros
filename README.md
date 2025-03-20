# Docker File for ROS2 Humble

This repo provides a Dockerized development environment for:
1. **ROS2(Humble)** setup.
2. **ROS2(Humble), Gazebo(Ignition) and PX4** integration setup.

---

## Repository Structure

- [`ros2-humble/`](https://github.com/Srindot/ROS-docker-setup/tree/main/ros2-humble) - Setup for ROS2 Humble.
- [`ros2-gazebo-px4/`](https://github.com/Srindot/ROS-docker-setup/tree/main/ros2_humble-px4-gazebo_ignition) - Setup for ROS2, Gazebo, and PX4 simulation.

---

## Cloning the Repository
For setting up the docker environment clone this repository:

```bash 
git clone https://github.com/Srindot/ROS-docker-setup.git
```

### 1. ROS2 Humble Setup
To build the Docker Image

Navigate to the ROS-docker-setup/ros2-humble folder:

```bash
cd ROS-docker-setup/ros2-humble
```
Build the docker file with the following command.

```bash 
docker build -t ros2humble:latest .
```
After building the docker image, a container can be created with the name as `myros` using the built image by the following command

```bash
docker run -it \
  --name myros \
 --privileged \
  -e DISPLAY=$DISPLAY \
  -e PULSE_SERVER=unix:/run/user/$(id -u)/pulse/native \
  --volume=/run/user/$(id -u)/pulse/native:/run/user/$(id -u)/pulse/native \
  --device /dev/snd \
  --group-add audio \
  --net=host \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume /home/$(whoami)/.Xauthority:/root/.Xauthority:ro \
  ros2humble:latest
```
To exit the container
```bash 
exit
```
To stop the container 

```bash
docker stop myros
```

To start the container again

```bash
docker start myros 
```

To enter to the bash 
``` bash
docker exec -it myros /bin/bash
```

To remove the container 

```bash 
rm -f myros
```

### 1. ROS2 Gazebo Humble Setup
To start off, navigate to Ros2 gazebo folder

```bash
cd ros2_humble-px4-gazebo_ignition
```

then, build the docker file 
``` bash 
docker build -t ros2gzpx4:latest .
```

After the image is built, run a contianer named `rosgzpx4` by the following command

```bash 
docker run -it \
  --name rosgzpx4 \
 --privileged \
  -e DISPLAY=$DISPLAY \
  -e PULSE_SERVER=unix:/run/user/$(id -u)/pulse/native \
  --volume=/run/user/$(id -u)/pulse/native:/run/user/$(id -u)/pulse/native \
  --device /dev/snd \
  --group-add audio \
  --net=host \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume /home/$(whoami)/.Xauthority:/root/.Xauthority:ro \
  ros2gzpx4:latest
```
To exit the container
```bash 
exit
```
To stop the container 

```bash
docker stop rosgzpx4
```

To start the container again

```bash
docker start rosgzpx4 
```

To enter to the bash 
``` bash
docker exec -it rosgzpx4 /bin/bash
```

To remove the container 

```bash 
rm -f rosgzpx4
```

### Note
Ensure your host system supports GUI applications (e.g., X11) for GUI tools to display correctly.

If you face any issues, please open an issue in GitHub.