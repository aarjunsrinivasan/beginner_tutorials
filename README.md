# ENPM808X - ROS Services, Logging ,ROSTEST, TF and ROSBAG ,and Launch files .

[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://github.com/aarjunsrinivasan/beginner_tutorials/blob/master/LICENSE)
---

An implementation of ROS subscriber publisher node using [ROS tutorial](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29)

Week9 Additions: Added a service stringupdate to update the default published text by the talker node.

Week10 Additions: Added Level 2 integration test for talker node stringupdate service. The software also has an implementation of tf broadcast of a /talk fram. The launch file is updated to provide functionality to record topics using rosbag.

Overall the software is simple tutorial showcasing the usage of various ROS functionalities and features. It has implementations of publisher subscriber, service, tf broadcast, rosbag and rostest.

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


## Running Demo using launch file
To run the demo using launch file type the following in a terminal
```
cd catkin_ws
source devel/setup.bash
roslaunch beginner_tutorials hw10.launch
```

again utilize ctrl+C to stop program in each of the 2 terminal.

## Modify default text using service
To modify the default text run the demo either using the launch file as mentioned above (or you can run the demo without the launch file as explained above)

After the demo starts open a new terminal and type
```
cd catkin_ws
source devel/setup.bash
rosservice call /stringupdate <your string>
```

You will notice that the default text changes to the text you have entered.

an example would be
```
rosservice call /stringupdate ENPM808X
```

## Change Loop frequency
To modify the loop frequency open run the demo using launch file using the following command
```
roslaunch beginner_tutorials hw9.launch frequency:=<int value greater than 0>
```

an example would be
```
roslaunch beginner_tutorials hw10.launch frequency:=5
```
## TF Frames
The talker.cpp node broadcasts the /talk frame which has a non-zero translation and rotation with respect to the /world frame. We can verify the TF frames using tf_echo and rqr_tf_tree.

The translation vector in this code is based on sine and cosine values of the ros::time, therefore with each loop run the translation value changes.
On running tf_echo it produces an terminal output showing the value of translation and rotational transformation vectors with each loop run in the talker node.

To use tf_echo run the software demo using launch file as mentioned above.
Open a new terminal and type
```
rosrun tf tf_echo /world /talk
```
The translation and rotation transform vectors are displayed in the terminal.
press ctrl+C in each terminal to stop the program.


The output will be something like this-
```
At time 1605046543.068
- Translation: [0.984, 0.176, 0.000]
- Rotation: in Quaternion [0.000, 0.000, 0.479, 0.878]
            in RPY (radian) [0.000, -0.000, 1.000]
            in RPY (degree) [0.000, -0.000, 57.296]
At time 1605046544.068
- Translation: [0.680, -0.733, 0.000]
- Rotation: in Quaternion [0.000, 0.000, 0.479, 0.878]
            in RPY (radian) [0.000, -0.000, 1.000]
            in RPY (degree) [0.000, -0.000, 57.296]
At time 1605046545.068
- Translation: [-0.250, -0.968, 0.000]
- Rotation: in Quaternion [0.000, 0.000, 0.479, 0.878]
            in RPY (radian) [0.000, -0.000, 1.000]
            in RPY (degree) [0.000, -0.000, 57.296]
At time 1605046546.068
- Translation: [-0.950, -0.313, 0.000]
- Rotation: in Quaternion [0.000, 0.000, 0.479, 0.878]
            in RPY (radian) [0.000, -0.000, 1.000]
            in RPY (degree) [0.000, -0.000, 57.296]

````

We can use rqt_tf_tree for visualizing the tree of frames being broadcasted.

With the demo running type the follwing in a new terminal to visualize the tree
```
rosrun rqt_tf_tree rqt_tf_tree
```

view_frames produces a diagram of the broadcasted frame.
With the demo running type the following in a new terminal
```
cd ~/catkin_ws
rosrun tf view_frames
```
A .pdf file named frames is generated with the diagram and can be found in the catkin_ws folder. The example frames.pdf file for this software can be found in the results folder.

the pdf can be viewed by entering the following in the terminal
```
evince frames.pdf
```
press ctrl+C to stop the program in each of the terminals.

## ROSTEST
To run the test for talker node modifyText service type the following in  terminal.
```
cd ~/catkin_ws
source devel/setup.bash
rostest beginner_tutorials talkerTest.launch 
```

example test output
```
... logging to /home/arjun/.ros/log/rostest-arjun-Legion-Y545-PG0-14532.log
[ROSUNIT] Outputting test results to /home/arjun/.ros/test_results/beginner_tutorials/rostest-test_talkerTest.xml
[ WARN] [1605046852.907823227]: User has changed the default message
[Testcase: testtalkerTest] ... ok

[ROSTEST]-----------------------------------------------------------------------

[beginner_tutorials.rosunit-talkerTest/testIfstringupdateExist][passed]
[beginner_tutorials.rosunit-talkerTest/testTalkerDefaultMessageUpdate][passed]

SUMMARY
 * RESULT: SUCCESS
 * TESTS: 2
 * ERRORS: 0
 * FAILURES: 0

rostest log file is in /home/arjun/.ros/log/rostest-arjun-Legion-Y545-PG0-14532.log

```

## ROSBAG
A .bag file recording all topic of duration 15 seconds is available in the results folder.
To run the listener node using the .bag file type the following in a new terminal.
```
roscore
```
After starting roscore open a new terminal and type the following
```
cd ~/catkin_ws
source devel/setup.bash
rosrun beginner_tutorials listener
```

Now open a new terminal and type the following.
```
cd ~/catkin_ws
source devel/setup.bash
cd src/beginner_tutorials/results
rosbag play recordtopics.bag
```

You can find the terminal running listener node displaying the recorded /chatter topic.

press ctrl+C in each of the terminal to exit the program.

To create a new bag file type
```
cd ~/catkin_ws
source devel/setup.bash
roslaunch beginner_tutorials hw10.launch rosbagEnable:=true
```

press ctrl+C in each terminal window to exit from the program and stop the recording.

the new rosbag file can be fould in the .ros directory
```
cd ~/.ros
rosbag info recordtopics.bag
```
the above command will list details about the message and topics recorded. This rosbag file can be played for the listener node (first start the listener node and roscore as mentioned earlier in ROSBAG section) using
```
rosbag play recordtopics.bag
```



