# usma_embedded_computer
Instructions on configuring an embedded computer such as a Raspberry Pi or Odroid

## Raspberry Pi 3 

### 1. Installing OS (Ubuntu MATE)
 *Our disk is going to be a microSDHC Card. Use one with memory greater than 8GB and speed class higher than 10. [[1]](https://ubuntu-mate.org/raspberry-pi/) [[2]] (https://www.youtube.com/watch?v=m5QXsKSwt-c)*
#### *To create the OS Disk using a Linux machine:*
- *Option 1*: Using the 'dd' utility in command line:
  - `sudo apt-get install gddrescue xz-utils`
  - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.1 LTS for Raspberry Pi. Once download is complete, the .xz file size should be about 1.1GB.
  - `cd Downloads/`
  - `unxz ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz`
  - The microSDHC Card maybe present as /sd**a** or /sd**b**. You can identify the device name by `ls /dev/sd*`
  - Once you've identified 'x' in /dev/sd**x**, run the following command by replacing 'x'.
  - `sudo ddrescue -D --force ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img /dev/sdx`
  - [Here's] (https://asciinema.org/a/34243) the complete recording of the terminal while executing these commands
  
- *Option 2*: Using a graphical tool:
  - `sudo apt-get install gnome-disk-utility`
  - After installation is complete, open the GUI and follow [these] (https://www.youtube.com/watch?v=V_6GNyL6Dac) steps on using the GNOME Disk utility to 'Restore Disk Image'
 
#### *To create the OS Disk using a Windows machine:*
 - Your SD Card, if not brand new, may have sector errors and odd partions. It is always advisable to format the drive before laying down the OS. You may download and use [this] (https://www.sdcard.org/downloads/formatter_4/) tool.  
 - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.1 LTS for Raspberry Pi.
 - Once download is complete, the .xz file size should be about 1.1GB. Use [7-Zip] (http://www.7-zip.org/) or [WinZip] (http://www.winzip.com/win/en/downwz.html) to extract the image.
 - Use [Win32 Disk Imager] (https://sourceforge.net/projects/win32diskimager/) to write the image onto the SD card.
 - Open Disk Imager and select path to the image you extracted in the above step. Also select the target device to write onto. This would be the drive corresponding to the SD Card reader (Example- F: or H:)

### 2. Initial setup 
- If this your first time with the RPi, you may find the first two pages of this [Quick Start Guide] (https://www.raspberrypi.org/qsg) useful. Ignore the SD Card setup portion, we are not utilizing NOOBS.
- On the first boot, the Pi will run through a setup wizard where you can create a user account. Please check with the OIC or Engineering Support Group personnel before creating the username and password. We follow a standard convention for ease of operation.
- The Wireless MAC Address of your device should be registered with the Computer Support Group to be able to connect to the EECSDS3 WiFi. This step is performed for devices issued in class or lab. If you have problems connecting, check with your OIC.

### 3. Install useful software and utilities
 - Install GNOME text editor: `sudo apt-get install gedit`
 - Install build essential: `sudo apt-get install build-essential -y`
 - Install SSH server: `sudo apt-get install openssh-server`
 - Install modem program: `sudo apt-get install minicom`
 - Install git commands: `sudo apt-get install git`
 
### 4. Install ROS (Optional)
- Follow instructions on [ROS Wiki] (http://wiki.ros.org/kinetic/Installation/Ubuntu) for installing the latest version of ROS i.e. Kinetic Kame. It is compatible with Ubuntu 15.10 and 16.04 LTS. 
- If you have an older platform such as Ubuntu 14.04 LTS, [ROS Indigo Igloo] (http://wiki.ros.org/indigo) is reccommended. [[g-r]] (http://www.german-robot.com/2016/05/26/raspberry-pi-sd-card-image/)

### 5. Pixy Cam (Optional)
1. Install dependencies:
 - `sudo apt-get install libusb-1.0-0.dev`  [[1]] (http://askubuntu.com/questions/629619/how-to-install-libusb)
 - `sudo apt-get install libboost-all-dev`
 - `sudo apt-get install cmake`

2. Download Pixy Source Code
 - `git clone https://github.com/charmedlabs/pixy.git`
 
3. Build & Install
 - `cd pixy/scripts`
 - `./build_libpixyusb.sh`
 - `sudo ./install_libpixyusb.sh`

4. Build and Run example script
 - `./build_hello_pixy.sh`
 - `cd ../build/hello_pixy`
 - `sudo ./hello_pixy`
 
5. Install PixyMon (Optional) [[1]] (http://cmucam.org/projects/cmucam5/wiki/Installing_PixyMon_on_Linux)
  - Install QT: `sudo apt-get install qt4-dev-tools`
  - `sudo apt-get install qt4-qmake`
  - `sudo apt-get install qt4-default`
  - Install G++ compiler: `sudo apt-get install g++`
  - Download Pixy source code: `git clone https://github.com/charmedlabs/pixy.git`
  - Run the build script: `cd pixy/scripts`
  - `./build_pixymon_src.sh`
  - Add permissions for Pixy USB Interface: `cd ../src/host/linux/`
  - `sudo cp pixy.rules /etc/udev/rules.d/`
  - To Open PixyMon, `cd ../../../build/pixymon/bin/`
  - `./PixyMon`
  - [Instructions](http://cmucam.org/projects/cmucam5/wiki/Teach_Pixy_an_object_2) to train the PixyCam through PixyMon
  
 

## Raspberry Pi 2

#### Configure embedded computer with Ubuntu and ROS (Raspberry Pi 2)
1. Install [Ubuntu 14.04 LTS] (https://wiki.ubuntu.com/ARM/RaspberryPi) on a microSD card (32GB is typically large enough).
 - These [instructions] (https://www.raspberrypi.org/documentation/installation/installing-images/linux.md) are helpful as well.
2. Connect your RPi2 using wired Ethernet.
 - If a wired connection is unavailable, use a USB-tether on a phone or hotspot.  Check with the CSG.
 - Set up your RPi2 interfaces to allow a USB tether:
 - `$ sudo nano /etc/network/interfaces`
  ```
  allow-hotplug usb0
  iface usb0 inet dhcp
  ```
3. Install linux-firmware drivers to enable wifi and ssh.
 - `sudo apt-get install linux-firmware`
 - `sudo apt-get install wicd`
 - `sudo apt-get install openssh-server`
4. Setup [wifi] (https://help.ubuntu.com/community/NetworkConfigurationCommandLine/Automatic) on your device.
 - Aother [reference] (https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/setting-up-wifi-with-occidentalis).
 - `sudo nano /etc/network/interfaces`
  ```
  auto wlan0
  allow-hotplug wlan0
  iface wlan0 inet dhcp
    wpa-ssid "EECSDS3"
    wpa-psk "accessgranted"
  ```
5. Make sure the wifi dongle is assigned wlan0. If not, you can change it under the udev rules:
 - `sudo nano /etc/udev/rules.d/70-persistent-net.rules`
6. Once connected to wifi, ensure you have performed the other [installs] (https://wiki.ubuntu.com/ARM/RaspberryPi):
 - Resize partition
 - Install swapfile
 - The serial console will be configed later.
 - GNOME is optional as well.
7. Install build essential:
 - `sudo apt-get install build-essential -y`
8. If you would like to set up ROS:
 - [Install ROS] (http://wiki.ros.org/indigo/Installation/UbuntuARM)
 - [Setup ROS Workspace] (http://wiki.ros.org/catkin/Tutorials/create_a_workspace)
