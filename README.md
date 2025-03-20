# Docker File for ROS2 Humble

This repo provides a Dockerized development environment for:
1. **ROS2(Humble)** setup.
2. **ROS2(Humble), Gazebo(Ignition) and PX4** integration setup.

---

## Repository Structure

- [`ros2-humble/`][https://github.com/Srindot/ROS-docker-setup/tree/main/ros2-humble] - Setup for ROS2 Humble.
- [`ros2-gazebo-px4/`][https://github.com/Srindot/ROS-docker-setup/tree/main/ros2_humble-px4-gazebo_ignition] - Setup for ROS2, Gazebo, and PX4 simulation.

---

## Cloning the Repository
For setting up the environment clone this repository:

```bash 
git clone https://github.com/Srindot/ROS-docker-setup.git
```

1. ROS2 Humble Setup
Building the Docker Image
Navigate to the ros2-humble folder:

bash
cd ros2-humble
Build the Docker image:

bash
docker build -t <image-name> .
Running the Docker Container
After the image is built, run the following command to start the ROS2 container:

bash
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
  <image-name>
Replace <image-name> with the tag you used during the Docker build.

2. ROS2 Gazebo and PX4 Setup
Building the Docker Image
Navigate to the ros2-gazebo-px4 folder:

bash'''
cd ros2-gazebo-px4
Build the Docker image:

bash
docker build -t <image-name> .
Running the Docker Container
After the image is built, run the following command to start the ROS2 Gazebo and PX4 container:

bash
docker run -it \
  --name myros-gazebo \
  --privileged \
  -e DISPLAY=$DISPLAY \
  -e PULSE_SERVER=unix:/run/user/$(id -u)/pulse/native \
  --volume=/run/user/$(id -u)/pulse/native:/run/user/$(id -u)/pulse/native \
  --device /dev/snd \
  --group-add audio \
  --net=host \
  --volume /tmp/.X11-unix:/tmp/.X11-unix \
  --volume /home/$(whoami)/.Xauthority:/root/.Xauthority:ro \
  <image-name>
Replace <image-name> with the tag you used during the Docker build.

Notes
Ensure your host system supports GUI applications (e.g., X11) for GUI tools to display correctly.

Use --privileged mode for containers requiring hardware/kernel access (e.g., PX4 simulations).

If you face any issues, please open an issue in GitHub.