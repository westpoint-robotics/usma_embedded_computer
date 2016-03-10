# usma_embedded_computer
Instructions on configuring an embedded computer such as a Raspberry Pi or Odroid

## Raspberry Pi 2

#### Configure embedded computer with Ubuntu and ROS (Raspberry Pi 2)
1. Install [Ubuntu 14.04 LTS] (https://wiki.ubuntu.com/ARM/RaspberryPi) on a microSD card (32GB is typically large enough).
 - These [instructions] (https://www.raspberrypi.org/documentation/installation/installing-images/linux.md) are helpful as well.
2. Connect your RPi2 using a wired Ethernet. 
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
(Make sure the wifi dongle is assigned wlan0 name.If not,then you can change it under the udev rules with following command. `sudo nano /etc/udev/rules.d/70-persistent-net.rules`
5. Once connected to wifi, ensure you have performed the other [installs] (https://wiki.ubuntu.com/ARM/RaspberryPi)
 - Resize partition
 - Install swapfile
 - The serial console will be configed later
 - GNOME is optional as well
Install build essential
 - `sudo apt-get install build-essential -y`
6. If you would like to set up ROS:
 - [Install ROS] (http://wiki.ros.org/indigo/Installation/UbuntuARM)
 - [Setup ROS Workspace] (http://wiki.ros.org/catkin/Tutorials/create_a_workspace)
