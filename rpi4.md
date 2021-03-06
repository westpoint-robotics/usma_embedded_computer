## Raspberry Pi 4 

### 1. Download preferred OS
- *Option 1 (Recommended)*: [32-bit Ubuntu MATE 20.04](https://releases.ubuntu-mate.org/focal/armhf/ubuntu-mate-20.04.1-beta2-desktop-armhf+raspi.img.xz) (Compatible with Raspberry Pi 3B, 3B+, 4B). Once download is complete, the .xz file size should be 1.1GB. 
- *Option 2*: [Raspberry Pi OS](https://downloads.raspberrypi.org/raspios_full_armhf_latest)(Formerly called Raspbian). [[1]](https://www.raspberrypi.org/downloads/raspberry-pi-os/)

### 2. Flash OS onto target disk
*Our disk is going to be a microSDHC Card. Use one with memory greater than 16GB and speed class higher than 10. [[2]](https://www.pidramble.com/wiki/benchmarks/microsd-cards) [[3]](https://www.youtube.com/watch?v=m5QXsKSwt-c)*
*Your SD Card, if not brand new, may have sector errors and odd partions. It is always advisable to format the drive before laying down the OS. You may download and use [this](https://www.sdcard.org/downloads/formatter_4/) tool.*

- *Option 1 (Recommended)*: Create the OS Disk using Etcher on a Windows machine:
  - Download and install [Etcher](https://github.com/balena-io/etcher/releases/download/v1.5.109/balenaEtcher-Setup-1.5.109.exe) to write the image onto the SD card. The target device to write onto would be the drive corresponding to the SD Card reader (Example- F: or H:)
- *Option 2*: Create the OS Disk using Etcher on a Linux machine:
  - Download and install [Etcher](https://github.com/balena-io/etcher/releases/download/v1.5.109/balena-etcher-electron-1.5.109-linux-x64.zip) to write the image onto the SD card. The target device to write onto would be the drive corresponding to the SD Card reader (/dev/media)
- *Option 3*: Create the OS Disk using [RPi Imager](https://www.raspberrypi.org/downloads/) on a Windows machine:
  - Download and install [Raspberry Pi Imager](https://downloads.raspberrypi.org/imager/imager_1.4.exe).
  - After installation is complete, open the GUI and follow [these](https://linuxhint.com/install_ubuntu_mate_raspberry_pi_4/) instructions.
- *Option 4*: Create the OS Disk using [RPi Imager](https://www.raspberrypi.org/downloads/) on a Linux machine:
  - Download and install Raspberry Pi Imager: `sudo apt install rpi-imager`.
  - After installation is complete, open the GUI and follow [these](https://linuxhint.com/install_ubuntu_mate_raspberry_pi_4/) instructions.

- *Troubleshooting*: If the RPi4 does not boot up after flashing the SD card with an OS, check out these pages for some common troubleshooting ideas:
  - [MakeUseOf](https://www.makeuseof.com/tag/raspberry-pi-wont-boot-fix/)
  - [Raspberry Pi Forum](https://www.raspberrypi.org/forums/viewtopic.php?t=244283)
  - [Pi Hut](https://support.thepihut.com/hc/en-us/articles/360001887937-My-Raspberry-Pi-4-will-not-boot-is-faulty)

### 3. Initial setup 
- On first boot, the RPi will run through a setup wizard where you can create a user account. Please check with the OIC before creating the username and password. We follow a standard convention for ease of operation.
- WREN_IoT: To be able to connect to this network, the wireless MAC Address of your device should be registered with the Computer Support Group or CIO/G6. Use the `ifconfig` command to display your device's MAC address. Provide your OIC with the MAC corresponding to the wireless interface.
- EECSnet: You will need to create user accounts to access this network wirelessly. To create an account and obtain login credentials, see your OIC.

### 4. Install useful software and utilities
- Type the following in a Terminal (Ctrl + Alt + T)
 - Install Terminator: `sudo apt-get install terminator ant`
 - Install GNOME text editor: `sudo apt-get install gedit meld gedit-plugins`
 - Install build essential: `sudo apt-get install gparted build-essential -y`
 - Install SSH server: `sudo apt-get install openssh-server`
 - Install modem program: `sudo apt-get install minicom`
 - Install git commands: `sudo apt-get install git gitk git-core git-doc`
 
### 5. System Settings -> Software & Updates
- 'Ubuntu Software' tab [[3]](https://help.ubuntu.com/community/Repositories/Ubuntu)
  - Check the top four boxes under 'Downloadable from the Internet': main, universe, restricted, multiverse.
- 'Updates tab'
  - Check te first two boxes: bionic-security and bionic-updates
  - 'Automatically check for updates: Never'
  - 'When there are security updates: Display Immediately'
  - 'When there are other updates: Display every two weeks'
  - 'Notify me of a new Ubuntu version: Never'
 
### 6. Install ROS (Optional)
- Follow instructions on [ROS Wiki](http://wiki.ros.org/noetic/Installation/Ubuntu) for installing the ROS Noetic. Download the 'full-desktop' version.
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
