# Turtlebot3-Rasberripy
Installation of turtlebot3 with Rasberry pi

## Installation

Based on http://emanual.robotis.com/

### Prerequisites

Turtlebot3, Rasberry pi, OpenCR board (all things are packaged in a Turtlebot3 box)

### Basic installation

* Assemble turtlebot3, Rasberry pi and OpenCR through manual.
* Boot Raseberry pi with micro SDCard. <br />
  *  There is a 8GB micro SDCard in a Turtlebot3 box. <br />
  *  SDCard is empty. Need download UBUNTU-MATE 16.04 for rasberry pi installation. <br />
     *  [Install UBUNTU-MATE](https://yeopbox.com/%EB%9D%BC%EC%A6%88%EB%B2%A0%EB%A6%AC%ED%8C%8C%EC%9D%B4-3-raspberry-pi%EC%97%90-%EC%9A%B0%EB%B6%84%ED%88%AC-%EB%A9%94%EC%9D%B4%ED%8A%B8-16-04-lts-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0/), [Rasberry pi setup](http://emanual.robotis.com/docs/en/platform/turtlebot3/raspberry_pi_3_setup/#install-linux-ubuntu-mate) <br />
* Follow [Remote PC setup](http://emanual.robotis.com/docs/en/platform/turtlebot3/pc_setup/).

* #### Make sure ROS packages are properly installed to Rasberry pi and Remote PC. <br />
  * If **"catkin_make"** command is completed without any errors, ROS is well installed.

### Network configuration

* Turtlebot3 can be connected to remote PC by wifi networks or ethernet cable. <br />
* To drive ROS for both components, they need to know other's ip network <br/> by setting "ROS_MASTER_URI" and "ROS_IP" at "~/.bashrc". <br />
* Turtlebot3 or Remote PC both can be "ROS_MASTER_URI". <br />
```
#### Remote PC master
At Remote PC "~/.bashrc", add
ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
ROS_IP=IP_OF_REMOTE_PC

At turtlebot3 "~/.bashrc", add
ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
ROS_IP=IP_OF_TURTLEBOT3

#### Turtlebot3 master
At Remote PC "~/.bashrc", add
ROS_MASTER_URI=http://IP_OF_TURTLEBOT3:11311
ROS_IP=IP_OF_REMOTE_PC

At turtlebot3 "~/.bashrc", add
ROS_MASTER_URI=http://IP_OF_TURTLEBOT3:11311
ROS_IP=IP_OF_TURTLEBOT3
```

* Make sure **"http://"** is only prefixed for **"ROS_MASTER_URI"**. **"http://"** should not be added to "ROS_IP" and "ROS_HOSTNAME"

* #### Connection by wifi networks <br />
  * For Linux installed Remote PC, need to setup [UBUNTU HOTSPOT](http://ubuntuhandbook.org/index.php/2016/04/create-wifi-hotspot-ubuntu-16-04-android-supported/) to communicate only with turtlebot3. <br />
  * After ubuntu hotspot setup, connect turtlebot3 to hidden wifi networks created by Remote PC. <br />
  * Check ip address of Remote PC and turtlebot3 by **"ifconfig"** command. <br />
  
* #### Connection by ethernet <br />
  * Connect Remote PC and rasberry pi by ethernet cable. <br/>
  * At Remote PC ethernet configuration, ipv4 window, set connection mode as **"share with other computers"**. <br />
    * This makes Remote PC and turtlebot3 connected by ethernet cable.
  * Check ip address of Remote PC and turtlebot3 by **"ifconfig"** command. <br />
  
* Check connection by **ssh** command. If connection is successfully setup, you can access to turtlebot3 with turtlebot3 ip address.  
  * Do not need connect monitor, keyboard and mouse to turtlebot3 anymore!
  


### OpenCR setupt with Arduino

* [OpenCR setup](http://emanual.robotis.com/docs/en/platform/turtlebot3/opencr_setup/#opencr-setup),  <br />
  * Make sure **jump_to_fw** text be printed. <br/>
  * Do not need to install Arduino on rasberry pi. Install Arduino on your Remote PC. [Arduino setup](http://emanual.robotis.com/docs/en/parts/controller/opencr10/#arduino-ide)(<br/>
  * Connect OpenCR to your Remote PC and run Arudino on your Remote PC.

* Before uploading **Examples/turtlebot3/turtlebot3_model/turtlebot3_core**, <br/>need to setup first DYNAMIXEL firmware on OpenCR. <br/>
  * If not, DYNAMIXEL will not move at all.
  
* In Arduino window, go to **Examples/turtlebot3/turtlebot3_setup/turtlebot3_motor_setup** and upload. <br/>
  * When setup DYNAMIXEL, need to connect only one DYNAMIXEL to OpenCR. <br/>Motor_setup firmware can not find two DYNAMIXELs at the same time. <br/>
  * Open serial monitor and check each DYNAMIXEL motor work successfully.
  * After setup two DYNAMIXELs, connect both DYNAMIXELs to OpenCR and upload **turtlebot3_core**.
  * After that, connect OpenCR to rasberry pi.
```
ssh turtlebot3_name@IP_OF_TURTLEBOT3
```
  

## Move Turtlebot3

### Bringup Turtlebot3
To move Turtlebot3, need to do **bringup** first to Turtlebot3

* Run **roscore** at master node
  * If **roscore** gives an error, check **"ROS_MASTER_URI"** and **"ROS_IP"** in ~/.bashrc at Remote PC and Turtlebot3
```
roscore
```
* [Bring up turtlebot3](http://emanual.robotis.com/docs/en/platform/turtlebot3/bringup/#bringup)
```
roslaunch turtlebot3_bringup turtlebot3_robot.launch
```
* [Teleoperation with keyboard or joystick](http://emanual.robotis.com/docs/en/platform/turtlebot3/teleoperation/#teleoperation)
  * When teleoperate with joystick, make sure joystic well connected via **ls /dev/input/js0 ** command


## Setup webcam to rasberry pi

* Install usb_cam ros package
```
cd ~/catkin_ws/src
git clone https://github.com/bosch-ros-pkg/usb_cam.git
cd ..
catkin_make(build again)
```


## Reference

1. [Turtlebot3 emanual](http://emanual.robotis.com/)
2. [Robotics blog](http://enssionaut.com/xe/board_robotics)



