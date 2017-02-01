# usma_embedded_computer
Instructions on configuring an embedded computer such as a Raspberry Pi or Odroid

## Raspberry Pi 3 

#### 1. Installing OS
 *Our disk is going to be a microSDHC Card. Use one with memory greater than 8GB and speed class higher than 10. [[1]](https://ubuntu-mate.org/raspberry-pi/)*
 
 *To create the OS Disk using a Linux machine:*
 - *Option 1*: Using the 'dd' utility in command line:
  - `sudo apt-get install gddrescue xz-utils`
  - `unxz ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz`
  - The microSDHC Card maybe present as /sda or /sdb. You can identify the device name with this command
  - `ls /dev/sd*`
  - Once you've identified 'x' in /dev/sdx, run the following command by replacing 'x'.
  - `sudo ddrescue -D --force ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img /dev/sdx`
  - [Here's] (https://asciinema.org/a/34243) the complete recording of the terminal while executing these commands
  
 - *Option 2*: Using a graphical tool:
  - `sudo apt-get install gnome-disk-utility`
  - After installation is complete, open the GUI and follow [these] (https://www.youtube.com/watch?v=V_6GNyL6Dac) steps on using the GNOME Disk utility to 'Restore Disk Image'
 
 *To create the OS Disk using a Windows machine:*
 - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.1 LTS for Raspberry Pi.
 - Once download is complete, the .xz file size should be about 1.1GB. Use [7-Zip] (http://www.7-zip.org/) or [WinZip] (http://www.winzip.com/win/en/downwz.html) to extract the image.
 - Use [Win32 Disk Imager] (https://sourceforge.net/projects/win32diskimager/) to write the image onto the SD card.
 - Open Disk Imager and select path to the image you extracted in the above step. Also select the target device to write onto. This would be the drive corresponding to the SD Card reader (Example- F: or H:)

#### 2. Initial setup 
- If this your first time with the RPi, you may find the first two pages of this [Quick Start Guide] (https://www.raspberrypi.org/qsg) useful. Ignore the SD Card setup portion, we are not utilizing NOOBS.
- On the first boot, the Pi will run through a setup wizard where you can create a user account. Please check with the OIC or ESG personnel before creating the username and password. We follow a standard convention for ease of operation.

#### 3. Install Linux drivers and utilities


#### 4. Install ROS 
- Follow instructions on [ROS Wiki] (http://wiki.ros.org/kinetic/Installation/Ubuntu). If you have doubts, check with the OIC. 


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
