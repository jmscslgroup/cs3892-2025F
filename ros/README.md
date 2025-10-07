# Running Docker

## Pull the Docker Image

```
docker pull sprinkjm/rosempty:latest
```

## First time only: create a place to connect docker to your host machine

Go to your `src` directory for the course, create the following folder

```
cd src
mkdir -p rossim/src
cd rossim/src
```

**FIRST TIME ONLY clone some example repositories that will help**

```
git clone https://github.com/jmscslgroup/subtractor
git clone https://github.com/jmscslgroup/odometer
git clone https://github.com/jmscslgroup/carsimplesimulink
git clone https://github.com/jmscslgroup/profproject
cd ..
```
Download the example test bagfile from Brightspace: it will be called `hwilexample.bag`. Once it is downloaded, copy the file in and call it `mytest.bag` in your `rossim` folder
```
cd ..
```
now you are back in your `rossim` folder

```
cp ../somewhere/else/hwilexample.bag mytest.bag
```

## Launch docker
Make sure you are in your `rossim` folder

```
docker run --mount type=bind,source=.,target=/ros/catkin_ws -it rosempty
```

Now, inside of your docker container, compile your Ros catkin workspace. Your cwd should be `/ros/catkin_ws`

```
catkin_make
```

# Run various Ros and Docker things

If you make a new tab, you can connect to your Docker and get a new terminal in:

## Run roscore
```
docker ps
```
This should allow you to see the running docker container. YMMV:

```
(base) sprinkle@Jonathan-Sprinkles-Laptop-1802 ros % docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED              STATUS          PORTS     NAMES
070c6ebeddab   rosempty   "/ros_entrypoint.sh …"   About a minute ago   Up 59 seconds             upbeat_wu
```

Inside that shell, type

```
roscore
```

This should produce the Ros whitepages:

```
root@070c6ebeddab:/ros/catkin_ws# roscore
... logging to /root/.ros/log/64a4d012-89a2-11f0-896e-667974bcf5be/roslaunch-070c6ebeddab-625.log
Checking log directory for disk usage. This may take a while.
Press Ctrl-C to interrupt
Done checking log file disk usage. Usage is <1GB.

started roslaunch server http://070c6ebeddab:43811/
ros_comm version 1.17.4


SUMMARY
========

PARAMETERS
 * /rosdistro: noetic
 * /rosversion: 1.17.4

NODES

auto-starting new master
process[master]: started with pid [633]
ROS_MASTER_URI=http://070c6ebeddab:11311/

setting /run_id to 64a4d012-89a2-11f0-896e-667974bcf5be
process[rosout-1]: started with pid [643]
started core service [/rosout]

```

## Connect to running container with a second command prompt:

Again, YMMV on the name of the container.
```
docker exec -it upbeat_wu /bin/bash
```

You should now see a root login. 

## Let's play a bagfile:

```
root@070c6ebeddab:/ros/catkin_ws# rosbag play mytest.bag 
[INFO] [1756999207.678035636]: Opening mytest.bag

Waiting 0.2 seconds after advertising topics... done.

Hit space to toggle paused, or 's' to step.
 [PAUSED ]  Bag Time: 1695917970.570366   Duration: 3.307744 / 581.976349               240.94 

```

## Let's see the data while it is running!

 Again, YMMV on the name of the container.
 ```
 docker exec -it upbeat_wu /bin/bash
 ```

 You should now see a root login. In that login, run
 
 ```
 rostopic echo /car/vel_x
 ```
 
 Probably you are seeing *mostly* 
 ```
 ---
 data: 0.0
 ---
 data: 0.0
 ---
 data: 0.0
 ---
 data: 0.0
 ---
 data: 0.0
 ---
 
 ```
 
 That's because the car doesn't move for awhile. Let's start the rosbag playback when the car starts to move! If you use the MATLAB plotting function, it will show you that happens about 

# Useful git repositories for simulation

Learn about these and other useful repositories using the links below.

* https://github.com/jmscslgroup/cs3891proj2023
* https://github.com/jmscslgroup/subtractor
* https://github.com/jmscslgroup/odometer
* https://github.com/jmscslgroup/profproject
* https://github.com/jmscslgroup/carsimplesimulink

