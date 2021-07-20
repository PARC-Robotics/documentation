# Getting Started In Simulation


In this tutorial, you will set your set up a directory on your ROS-enabled PC as your workspace for development and install the competition ROS packages. Please follow the instructions below carefully.

!!! note
    This can ONLY be completed after you have set up your PC (by following the [Setting up your PC tutorial](../getting-started/setting-up-your-pc/index.md)).
    
    If you have already set up your PC and `catkin_ws`, skip to [Install TurtleBot3 packages](getting-started-simulation.md#install_turtlebot3_packages_via_debian_packages)

### Setup ROS workspace (Only if you don't already have a catkin_ws)

Open a new terminal on your PC, then copy and paste the following one line at a time:
```sh
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
```

### Install TurtleBot3 packages via Debian packages

```
sudo apt-get update
sudo apt-get install ros-melodic-dynamixel-sdk
sudo apt-get install ros-melodic-turtlebot3-msgs
sudo apt-get install ros-melodic-turtlebot3
```

### Clone the repository

In the same terminal (or in a new one), copy and paste the following:
```sh
cd ~/catkin_ws/src
git clone --recurse-submodules https://github.com/PARC-Robotics/PARC-Engineers-League-Phase2.git
```
Or if you already have cloned the repo without submodules, run command `git submodule update --init --recursive` to update them.

### Install dependencies

In the same terminal (or in a new one), copy and paste the following:
```sh
cd ~/catkin_ws
sudo apt update
rosdep install --from-paths ./src --ignore-src -y
```

### Compile packages
```sh
cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash
```


**NOTE:** There is a known issue while compiling, ` Intel RealSense SDK 2.0 is missing`  
To solve, update the file `realsense-ros/realsense_camera/CMakeLists.txt`,line: 43 to `find_package(realsense2 2.36.0)`
i.e. downgrade the required version of `realsense2` to `2.36.0`


### Set up ROS environment
To set the environment every time you launch a new terminal, following this command:

```sh
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

As you develop, it is good to set the environment variables whenever you run a `catkin_make` command to compile changes to your packages. You can do that by:
```sh
source ~/catkin_ws/devel/setup.bash
```


### Test installation

If you completed the preceding tasks successfully, you should be able to run this ROS launch command and see the Gazebo simulator and RViz simulator open with the following display:
```sh
roslaunch turtlebot3_parc turtlebot3_parc.launch
```
![Gazebo Simulator window](media/gazebo.png)
Gazebo Simulator window


![RViz window](media/rviz.png)
RViz window



### Controlling the robot using keyboard
Run the following command in a new terminal
```sh
source ~/catkin_ws/devel/setup.bash
roslaunch turtlebot3_parc teleop.launch
```

Now keeping the second terminal on top (teleop.launch) press `i` to move the robot forward, you can see the robot moving in "RViz" and "Gazebo" windows.
you can use the keys shown below to move the robot and `k` key to stop the movement.
```sh
Moving around:
   u    i    o
   j    k    l
   m    ,    .
```