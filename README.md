HBRS Cartesian Trajectory Controller
====================================

This [ROS node](http://www.ros.org/wiki/ROS/Tutorials/UnderstandingNodes) is designed to take a series of points along a trajectory that you want your robot arm to be able to follow. It will compute a path from the current position of the arm to the desired goal and attempt to follow it as closely as possible. 

### Available Services
* `/compute_trajectory` This service will take in a series of WayPoints (**must be more than zero(0)** ) and it will attempt to draw a straight line between the current gripper and the series of waypoints. It is currently setup so that we will allow the gripper to finish to within a tolerance of `0.003m` or `3mm`.

## Launching It Simulation:

This will bring up everything you need in order to set up the robot in simulation and to move and track its output. This will also launch [RVIZ](http://www.ros.org/wiki/rviz) which will visualize the points and both the ideal trajectory and the actual trajectory that the robot ended up following while executing the trajectory. 

* Start the Simulation: `$ roslaunch raw_bringup_sim robot.launch`
* Start the Trajectory Controller: `$ roslaunch hbrs_cartesian_trajectory_controller cartesian_trajectory_controller_offline.launch`

## Launching It Real Hardware:

This will launch the actual [youBot](http://youbot-store.com/) and initialize it and launch the componenet from a remote machine (if you do this the youbot needs to be set to your `ROS_MASTER`). It will also launch [RVIZ](http://www.ros.org/wiki/rviz) which will allow you to visualize the output from the robot with a slight delay depending on your setup. 

* Start the Robot: `$ roslaunch raw_bringup robot.launch`
* Start the Trajectory Controller: `$ roslaunch hbrs_cartesian_trajectory_controller cartesian_trajectory_controller_offline.launch`

## Running It: 
In order to start the HBRS Cartesian Trajectory Controller you need to call the service which is provides in the following way from the terminal: 

`$ rosservice call /compute_trajectory [waypoints]`

### WayPoint List
The input arguments take in a [PoseArray](http://www.ros.org/doc/api/geometry_msgs/html/msg/PoseArray.html) which lists out in order all of the poses that you want to reach using the arm. 

## Environment Variables
This requires the following environment variables to be present in your bashrc file: 
* `export ROBOT=youbot-hbrs1`

## Testing

In order to test the pacakge go into the `/ros/test` directory and run the following command: 

`$ ./test_trajectories.sh`
