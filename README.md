# Carla-Autoware.universe bridge


## Objective ##
This repo provides a bridge between Carla simulator(0.9.15) and Autoware.Universe. 

## Dependencies ##
The dependencies to install can be found in this [repo](https://github.com/rohanNkhaire/ros-bridge.git).
```bash
pip3 install -r requirements.txt
```

## Installation ##
The Repositories required to successfully run Carla and Autoware are :-
- [ros-bridge](https://github.com/rohanNkhaire/ros-bridge.git)
    - This is the main repo used to run a ROS2 bridge for Carla simulator.
- [carla_autoware](https://github.com/rohanNkhaire/carla_autoware)
    - This repo contains nodes to transfer required information to Autoware.Universe's stack.
- [carla_autoware_launch](https://github.com/rohanNkhaire/carla_autoware_launch)
    - This repo contains launch files to start the Carla simulation.
- [astuff_messages](https://github.com/rohanNkhaire/astuff_sensor_msgs.git)
    - Contains *derived_object_msgs* for *ros-bridge* to output spawned actors of Carla as ROS message.
- [autoware_auto_msgs](https://github.com/rohanNkhaire/autoware_auto_msgs.git)
    - This repo is required to transfer required messages to Autoware.Universe.


## Usage ##
```bash
# Clone the repo
git clone https://github.com/rohanNkhaire/carla_autoware_bridge.

# Set up a dir
cd carla_autoware_bridge
mkdir src
# We use --recursive tag to clone the carla_msgs submodule
vcs import src < bridge.repos --recursive

# First, source your ROS Galactic
source /opt/ros/humble/setup.bash

# Install dependencies
rosdep install --from-paths src -y --ignore-src

# Build the workspace
colcon build

# install dependencies for carla's python API
cd src/ros-bridge
pip3 install -r requirements.txt
```

## Run an example ##
```bash
# Host 1 - carla_autoware_bridge (Ubuntu 20.04)
source install/setup.bash
ros2 launch carla_autoware_launch carla_autoware.launch.xml
```

```bash
# Host 2 - Autoware.Universe (Ubuntu 22.04)
source install/setup.bash
ros2 launch autoware_launch autoware.launch.xml
```

## Note ##
This repo is tested on **ROS Humble**.

The setup was tested as
- Carla autoware bridge on Ubuntu 22.04(ROS Galactic)
- Autoware.universe on ubuntu 22.04(ROS Humble)

The main bridging component comes from [ros-bridge](https://github.com/carla-simulator/ros-bridge) repo. Check it out.

To use Ackermann control in ros-bridge, install a specific version of *simple-pid*
```bash
pip3 install simple-pid==1.0.1
```

# Digital Twin and Virtual Reality for Autonomous Vehicles #
Please checkout my work situated in [this](https://github.com/rohanNkhaire/carla_autoware/tree/digital_twin) repo.

