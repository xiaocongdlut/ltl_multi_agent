# 加入了 https://github.com/ethz-asl/rotors_simulator.git 无人机仿真，换了城市地图

# Reactive Task Allocation and Planning for Quadrupedal and Wheeled Robot Teaming
## Overview
This repo contains all the packages for multi-agent task allocation and planning based on Linear Temporal Logic (LTL). 
Each component is maintained individually. To run the simulation, ROS melodic and gazebo11 are suggested.

## Packages
This metapackage is composed of the following packages.

- **[ltl_planning_core](/ltl_planning_core)**: A metapackage in charge of multi-robot task allocation and planning.

- **[ltl_automation_a1](/ltl_automation_a1)**: Behavior tree nodes for online task execution. Quadruped and wheeled robots are both included.

- **[quadruped_sim](/quadruped_sim)**: Essential components for quadruped including Gazebo simulation, navigation, and low-level control. Make sure you have [Cheetah-Software](https://github.com/GTLIDAR/Cheetah-Software) installed before building the package.

- **[motion_capture_simulator](/motion_capture_simulator)**:

- **[ubtna_gazebo_pkg](/ubtna_gazebo_pkg)**: Essential components for wheeled robots from UBTECH including Gazebo simulation, navigation

- **[Groot](/Groot) (optional)**: GUI for behavior tree
 

## Installation
Before building the whole workspace, make sure `quadruped_ctrl` package is built successfully which is inside quadruped_sim folder.

All packages shall be located in the same catkin workspace. To build the packages, follow:
```
$ cd catkin_ws/src
$ git clone --recurse-submodules https://github.com/GTLIDAR/ltl_multi_agent
$ cd ..
$ rosdep install --from-paths src --ignore-src -r -y
$ catkin build
$ source devel/setup.bash
```

## Usage
Run a case study that involves a quadruped A1, a delivery robot DR and a walk training robot Wassi (DR and Wassi models
are proprietary and presented by a simple model):

In terminal 1, start gazebo simulation and BT nodes for each robot. Try rerunning the launch file if models
are not spawned correctly (to be fixed).
```
$ roslaunch ltl_automaton_planner study_2.launch
```

In terminal 2, start quadruped controller:
```
$ rosrun quadruped_ctrl a1_servo /cmd_vel:=/a1_gazebo/cmd_vel
```

In terminal 3, start LTL planner if quadruped stands up and laser scans are received in Rviz:
```
$ rosrun ltl_automaton_planner robot_planner_node_exp
```

## Reference Citation
To cite this work:
```
@inproceedings{zhou2022reactive,
  title={Reactive Task Allocation and Planning for Quadrupedal and Wheeled Robot Teaming},
  author={Zhou, Ziyi and Lee, Dong Jae and Yoshinaga, Yuki and Balakirsky, Stephen and Guo, Dejun and Zhao, Ye},
  booktitle={2022 IEEE 18th International Conference on Automation Science and Engineering (CASE)},
  pages={2110--2117},
  year={2022},
  organization={IEEE}
}
```

