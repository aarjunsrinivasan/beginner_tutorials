# ENPM808X - ROS Beginner tutorial Implementation of Publisher Subscriber.
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
---

An implementation of ROS subscriber publisher node using [ROS tutorial](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29)

## Pre-requisite
The project requires ROS melodic and catkin, and is developed on UBUNTU 18.04 LTS.

To install ROS please follow the tutorial [Link](http://wiki.ros.org/melodic/Installation/Ubuntu)


## How to build
Before building please ensure ROS melodic and catkin are installed.  
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash
cd src/
git clone https://github.com/aarjunsrinivasan/beginner_tutorials.git
cd ..
catkin_make
```
## Running Demo without launch file
To run the demo open a new terminal and type
```
roscore
```

To run talker open a new terminal and type
```
cd catkin_ws
source devel/setup.bash
rosrun beginner_tutorials talker
```

To run listener open a new terminal and type
```
cd catkin_ws
source devel/setup.bash
rosrun beginner_tutorials listener
```
To stop the program press ctrl+C in each of the three terminals.



