Introduction:
=============
(By Jiang Jun, August, 6th, 2018)

- This is the main program of Jiang's master research on "Glass confidence map building using laser rangefinder for mobile robots"
- The program can build a glass map of an indoor environment, showing glass as occupied on the map and all the objects' probability of being glass.
- The program is supposed to be run together with a SLAM algorithm, on a mobile robot equipped with a laser rangefider(LRF)


About how to use this program:
==============================
 
1. Preparations:
----------------
*** For running the program using data I recorded by rosbag:

- Operating system: Ubuntu 16.04
- Install Robot Operating System (ROS) Kinetic; build a catkin workspace
- Download the source code of ros package "gmapping" from its github (https://github.com/ros-perception/slam_gmapping) to your "~/catkin_ws/src" dirctory
- Go to gmapping's directory, open file "slam_gmapping/gmapping/src/slam_gmapping.cpp", comment line 755 and uncomment line 754. Also, go to line 240, change "occ_thresh_ = 0.25;" to "occ_thresh_ = 0.0;" 
	(or you can find one modified file directly in dirctory "~/catkin_ws/src/test/scripts")
- Move the folder "tests" to your ros "~/catkin_ws/src" dirctory ("tests" is also a ros package)
- Compile the ros packages using "catkin_make" (please refer: http://wiki.ros.org/catkin/commands/catkin_make)
- If errors appear, probably you are missing some dependent packages. Just intall the ones the error information tells you.
- If needed, go to "~/catkin_ws/src/tests/scripts", change all the ".py" files' properities by command "chmod +x *.py"
 
*** For running the program in new environments, you need to finish the above items and also need:

- A mobile robot and corresponding softwares which can provide odometry information to gmapping 
	(I used Pioneer 3DX + ros packages "Rosaria" and "turtlebot")
- A 2-D Laser Rangefinder and corresponding softwares which can provide LRF intensity and distance data to gmapping 
	(I used Hokuyo utm-30lx-ew + ros packages "urg_node")


2. Run the program using recorded data:
---------------------------------------
- Go to dirctory "~/catkin_ws/src/test/scripts"
- Open a terminal, run command "roslaunch tests gmapping_rosbag.launch"
	---> gmapping starts running, with rviz showing an unfiltered occupancy grid map and robot pose in it.
	
- Open a new terminal tab, run "python GlassMapOnLineTest.py" (within "~/catkin_ws/src/test/scripts")
	---> glass mapping program starts running, with the built glass map shown in a new window 

- Once the robot finish moving in the environment, "Ctrl+c" in the terminal running "python GlassMapOnLineTest.py"
	---> two maps pop up
	---> one is occupancy grid map (black in occupied grids) of the environment 
	---> the other map is the glass confidence map (blue or red in occupied grids)

- If you want to change the rosbag file, go to "tests/scripts/gmapping_rosbag.launch", find " <arg name="bag_name"  default="modi_B11F2"/>  ". The "modi_B11F2" here is the bag name currently used. Other usable bags can be found in "tests/bags" 

- If you want to stop the "python GlassMapOnLineTest.py", you need to close all the windows it generated.


3. Run the program using new data collected by a robot and a LRF:
----------------------------------------------------------------
- At the beginning, run "roslaunch tests gmapping_robotLRF.launch" instead of "roslaunch tests gmapping_rosbag.launch"
- The rest is same with "using recorded data"

