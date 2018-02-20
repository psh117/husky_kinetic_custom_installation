# husky_kinetic_custom_installation
Clearpath Husky system installation with Ubuntu 16.04 and ROS Kinetic


* Install Ubuntu 16.04
* Install ROS Kinetic [link to installation wiki](http://wiki.ros.org/kinetic/Installation)

* Install prerequisite packages
```sh
sudo apt install ros-kinetic-lms1xx ros-kinetic-ur5-description ros-kinetic-controller-manager ros-kinetic-robot-localization ros-kinetic-interactive-marker-twist-server ros-kinetic-twist-mux ros-kinetic-joy ros-kinetic-teleop-twist-joy ros-kinetic-joint-state-controller ros-kinetic-diff-drive-controller
```
* Clone some packages to catkin_ws
```sh
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
git clone https://github.com/husky/husky
git clone https://github.com/husky/husky_robot
cd ~/catkin_ws
catkin_make
```

* Create an udev rule for Husky connetion
```sh
sudo vi /etc/udev/rules.d/90-clearpath.rules
```
```
# Udev rule for the Prolific Serial-to-USB adapter shipped standard with Husky
SUBSYSTEMS=="usb", ATTRS{manufacturer}=="Prolific*", SYMLINK+="prolific prolific_$attr{devpath}", MODE="0666"
```
```sh
sudo udevadm control --reload-rules && sudo service udev restart && sudo udevadm trigger
```

## How to setup a Dualshock 4 wireless controller 
* Reference: https://github.com/ros-drivers/joystick_drivers/issues/84
* Install some packages
```sh
sudo apt install python-pip
sudo pip install ds4drv
```
* Pair your Dualshock 4 controller
* Create or copy the udev file (https://github.com/chrippa/ds4drv/blob/master/udev/50-ds4drv.rules)
```sh
sudo vi /etc/udev/rules.d/49-ds4drv.rules
```
```
KERNEL=="uinput", MODE="0666"
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="05c4", MODE="0666"
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", KERNELS=="0005:054C:05C4.*", MODE="0666"
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="09cc", MODE="0666"
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", KERNELS=="0005:054C:09CC.*", MODE="0666"
```

* Reload udevadm
```sh
sudo udevadm control --reload-rules && sudo udevadm trigger
```
* Run ds4drv
```sh
ds4drv --hidraw
```
