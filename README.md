# husky_kinetic_custom_installation
Clearpath Husky system installation with Ubuntu 16.04 and ROS Kinetic


* Install Ubuntu 16.04

* Create an udev rule for Husky connetion
```sh
sudo vi /etc/udev/rules.d/90-clearpath.rules
```
```
# Udev rule for the Prolific Serial-to-USB adapter shipped standard with Husky
SUBSYSTEMS=="usb", ATTRS{manufacturer}=="Prolific*", SYMLINK+="prolific prolific_$attr{devpath}", MODE="0666"
```

sudo vi 

```sh
sudo apt install ros-kinetic-robot-localization ros-kinetic-interactive-marker-twist-server ros-kinetic-twist-mux ros-kinetic-joy ros-kinetic-teleop-twist-joy ros-kinetic-joint-state-controller ros-kinetic-diff-drive-controller
```
