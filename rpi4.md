## Raspberry Pi 4 

### 1. Installing OS (Ubuntu MATE)
 *Our disk is going to be a microSDHC Card. Use one with memory greater than 8GB and speed class higher than 10. [[1]](https://ubuntu-mate.org/raspberry-pi/) [[2]](https://www.youtube.com/watch?v=m5QXsKSwt-c)*
 - Your SD Card, if not brand new, may have sector errors and odd partions. It is always advisable to format the drive before laying down the OS. You may download and use [this](https://www.sdcard.org/downloads/formatter_4/) tool. 
 
#### *To create the OS Disk using a Windows machine (Recommended):*
 - [Download]() Ubuntu MATE 18.04 for Raspberry Pi. Once download is complete, the .xz file size should be about 1.2GB.
 - Use [Etcher](https://github.com/resin-io/etcher/releases/download/v1.3.1/Etcher-Setup-1.3.1-x64.exe) to write the image onto the SD card. The target device to write onto would be the drive corresponding to the SD Card reader (Example- F: or H:)
 
#### *To create the OS Disk using a Linux machine:*
- *Option 1*: Using Etcher (Recommended):
  - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04.2-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.2 LTS for Raspberry Pi. Once download is complete, the .xz file size should be about 1.2GB.
  - Use [Etcher](https://github.com/resin-io/etcher/releases/download/v1.3.1/etcher-1.3.1-linux-x86_64.zip) to write the image onto the SD card. The target device to write onto would be the drive corresponding to the SD Card reader (/dev/media)
- *Option 2*: Using a Gnome utility:
  - `sudo apt-get install gnome-disk-utility`
  - After installation is complete, open the GUI and follow [these](https://www.youtube.com/watch?v=V_6GNyL6Dac) steps on using the GNOME Disk utility to 'Restore Disk Image'

### 2. Initial setup 
- If this your first time with the RPi, you may find the first two pages of this [Quick Start Guide](https://www.raspberrypi.org/qsg) useful. Ignore the SD Card setup portion, we are not utilizing NOOBS.
- On the first boot, the Pi will run through a setup wizard where you can create a user account. Please check with the OIC before creating the username and password. We follow a standard convention for ease of operation.
- EECSDS3 WiFi: The Wireless MAC Address of your device should be registered with the Computer Support Group to be able to connect to the EECSDS3. Use the `ifconfig` command to display your device's MAC address. Provide your OIC with the MAC corresponding to the wireless interface.
- EECSnet WiFi: You will need to create user accounts to access this network. To create an account and obtain login credentials, see your OIC.

### 3. Install useful software and utilities
- Type the following in a Terminal (Ctrl + Alt + T)
 - Install GNOME text editor: `sudo apt-get install gedit`
 - Install build essential: `sudo apt-get install build-essential -y`
 - Install SSH server: `sudo apt-get install openssh-server`
 - Install modem program: `sudo apt-get install minicom`
 - Install git commands: `sudo apt-get install git`
 - `sudo apt-get install bash-completion`
 
### 4. System Settings
- Check boxes for sources of software - main, canonical, multiverse
- Disable automatic updates
 - Go to 'System -> Administration -> Software & Updates -> Updates' and set the following:
 - 'Automatically check for updates: Never'
 - 'When there are security updates: Display Immediately'
 - 'When there are other updates: Display every two weeks'
 
### 5. Install ROS (Optional)
- Follow instructions on [ROS Wiki](http://wiki.ros.org/melodic/Installation/Ubuntu) for installing the ROS Melodic. Download the 'full-desktop' version.
- After ROS installation is complete, install additional tools: `sudo apt-get install git-core python-argparse python-wstool python-vcstools python-rosdep ros-kinetic-control-msgs ros-kinetic-joystick-drivers`
- Create ROS workspace:
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws/
catkin_make
echo "source $HOME/catkin_ws/devel/setup.bash" >> ~/.bashrc
source $HOME/catkin_ws/devel/setup.bash
rospack profile
```
