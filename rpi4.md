## Raspberry Pi 4 

### 1. Installing OS (Ubuntu MATE 32-bit)
 *Our disk is going to be a microSDHC Card. Use one with memory greater than 16GB and speed class higher than 10. [[1]](https://www.pidramble.com/wiki/benchmarks/microsd-cards) [[2]](https://www.youtube.com/watch?v=m5QXsKSwt-c)*
 - Your SD Card, if not brand new, may have sector errors and odd partions. It is always advisable to format the drive before laying down the OS. You may download and use [this](https://www.sdcard.org/downloads/formatter_4/) tool. 
 
#### *To create the OS Disk using a Windows machine (Recommended):*
 - [Download](https://releases.ubuntu-mate.org/bionic/armhf/ubuntu-mate-18.04.2-beta1-desktop-armhf+raspi-ext4.img.xz) Ubuntu MATE 18.04.2 32-bit (Compatible with Raspberry Pi 3B, 3B+, 4B). Once download is complete, the .xz file size should be about 1.2GB.
 - Use [Etcher](https://github.com/balena-io/etcher/releases/download/v1.5.109/balenaEtcher-Setup-1.5.109.exe) to write the image onto the SD card. The target device to write onto would be the drive corresponding to the SD Card reader (Example- F: or H:)
 
#### *To create the OS Disk using a Linux machine:*
- *Option 1*: Using Etcher (Recommended):
  - [Download](https://releases.ubuntu-mate.org/bionic/armhf/ubuntu-mate-18.04.2-beta1-desktop-armhf+raspi-ext4.img.xz) Ubuntu MATE 18.04.2 __32-bit__ (Compatible with Raspberry Pi 3B, 3B+, 4B). Once download is complete, the .xz file size should be about 1.2GB.
  - Use [Etcher](https://github.com/balena-io/etcher/releases/download/v1.5.109/balena-etcher-electron-1.5.109-linux-x64.zip) to write the image onto the SD card. The target device to write onto would be the drive corresponding to the SD Card reader (/dev/media)
- *Option 2*: Using a Gnome utility:
  - `sudo apt-get install gnome-disk-utility`
  - After installation is complete, open the GUI and follow [these](https://www.youtube.com/watch?v=V_6GNyL6Dac) steps on using the GNOME Disk utility to 'Restore Disk Image'

### 2. Initial setup 
- If this your first time with the RPi, you may find the first two pages of this [Quick Start Guide](https://www.raspberrypi.org/qsg) useful. Ignore the SD Card setup portion, we are not utilizing NOOBS.
- On the first boot, the Pi will run through a setup wizard where you can create a user account. Please check with the OIC before creating the username and password. We follow a standard convention for ease of operation.
- WREN_IoT: To be able to connect to this network, the wireless MAC Address of your device should be registered with the Computer Support Group or CIO/G6. Use the `ifconfig` command to display your device's MAC address. Provide your OIC with the MAC corresponding to the wireless interface.
- EECSnet: You will need to create user accounts to access this network wirelessly. To create an account and obtain login credentials, see your OIC.

### 3. Install useful software and utilities
- Type the following in a Terminal (Ctrl + Alt + T)
 - Install Terminator: `sudo apt-get install terminator ant`
 - Install GNOME text editor: `sudo apt-get install gedit meld gedit-plugins`
 - Install build essential: `sudo apt-get install gparted build-essential -y`
 - Install SSH server: `sudo apt-get install openssh-server`
 - Install modem program: `sudo apt-get install minicom`
 - Install git commands: `sudo apt-get install git gitk git-core`
 - `sudo apt-get install bash-completion`
 
### 4. System Settings -> Software & Updates
- 'Ubuntu Software' tab [[3]](https://help.ubuntu.com/community/Repositories/Ubuntu)
  - Check the top four boxes under 'Downloadable from the Internet': main, universe, restricted, multiverse.
- 'Updates tab'
  - Check te first two boxes: bionic-security and bionic-updates
  - 'Automatically check for updates: Never'
  - 'When there are security updates: Display Immediately'
  - 'When there are other updates: Display every two weeks'
  - 'Notify me of a new Ubuntu version: Never'
 
### 5. Install ROS (Optional)
- Follow instructions on [ROS Wiki](http://wiki.ros.org/melodic/Installation/Ubuntu) for installing the ROS Melodic. Download the 'full-desktop' version.
- After ROS installation is complete, install additional tools: `sudo apt-get install python-argparse python-wstool python-vcstools python-rosdep python-rosinstall-generator`
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
