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
* To drive ROS for both components, they need to know other's ip network by setting "ROS_MASTER_URI" and "ROS_IP" at "~/.bashrc". <br />
* Turtlebot3 or Remote PC both can be "ROS_MASTER_URI". <br />
  1. #### Remote PC master 
```
At Remote PC "~/.bashrc", add
ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
ROS_IP=IP_OF_REMOTE_PC

At turtlebot3 "~/.bashrc", add
ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
ROS_IP=IP_OF_TURTLEBOT3
``` 
  2. #### Turtlebot3 master
```
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


## OpenCR setupt with Arduino

* [OpenCR setup](http://emanual.robotis.com/docs/en/platform/turtlebot3/opencr_setup/#opencr-setup),  <br />
  * Make sure **jump_to_fw** text be printed. <br/>
  * Do not need to install Arduino on rasberry pi. Install Arduino on your Remote pc. [Arduino setup](http://emanual.robotis.com/docs/en/parts/controller/opencr10/#arduino-ide)(<br/>
  * Connect OpenCR to your Remote pc and run Arudino on your Remote PC.

* Before uploading **Examples/turtlebot3/turtlebot3_model/turtlebot3_core**, need to setup first DYNAMIXEL firmware on OpenCR. <br/>
  * If not, DYNAMIXEL will not move at all.
  
* In Arduino window, go to **Examples/turtlebot3/turtlebot3_setup/turtlebot3_motor_setup** and upload. <br/>
  * When setup DYNAMIXEL, need to connect only one DYNAMIXEL to OpenCR. Motor_setup firmware can not find two DYNAMIXEL at the same time. <br/>
  * Open serial monitor and check each DYNAMIXEL motor work successfully.
  * After setup two DYNAMIXELs, connect both DYNAMIXELs to OpenCR and upload **turtlebot3_core**.
  
  
  

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
