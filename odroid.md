# --- Odroid as Turtlebot2 computer ---

### 1. Installing OS (Ubuntu MATE)
 *Our disk is going to be an eMMC Card. Use one with memory greater than 16GB. [[1]](https://ubuntu-mate.org/raspberry-pi/) [[2]](https://www.youtube.com/watch?v=m5QXsKSwt-c)*
 - Your eMMC is not brand new, it may have sector errors and odd partions. It is always advisable to format the drive before laying down the OS. You may download and use [this](https://www.sdcard.org/downloads/formatter_4/) tool. 
 
#### *To create the OS Disk using a Windows machine (Recommended):*
 - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04.2-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.2 LTS for Raspberry Pi. Once download is complete, the .xz file size should be about 1.2GB.
 - Use [Etcher](https://github.com/resin-io/etcher/releases/download/v1.3.1/Etcher-Setup-1.3.1-x64.exe) to write the image onto the eMMC. The target device to write onto would be the drive corresponding to the SD Card reader / USB adapter (Example- F: or H:)
 
#### *To create the OS Disk using a Linux machine:*
 - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04.2-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.2 LTS for Raspberry Pi. Once download is complete, the .xz file size should be about 1.2GB.
 - Use [Etcher](https://github.com/resin-io/etcher/releases/download/v1.3.1/etcher-1.3.1-linux-x86_64.zip) to write the image onto the SD card. The target device to write onto would be the drive corresponding to the SD Card reader / USB adapter (/dev/media)
 
#### *To Clone from another SD Card:*- 
- *On Ubuntu-* [Steps](http://askubuntu.com/questions/227924/sd-card-cloning-using-the-dd-command) to clone an image already installed on another fully-operational SD Card. If you have only a single SD Card reader/slot on your PC, follow [these](http://askubuntu.com/questions/753977/cloning-an-sd-card-to-another-in-ubuntu-using-a-single-sd-card-reader) instructions.
- *On Windows-* [Steps](https://computers.tutsplus.com/articles/how-to-clone-your-raspberry-pi-sd-cards-with-windows--mac-59294) to clone Raspberry Pi SD Card using Windows

### 2. Initial setup 
- On the first boot, Ubuntu will run through a setup wizard where you can create a user account. Please check with the OIC before creating the username and password. We follow a standard convention for ease of operation.
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
- If you are connected to EECSDS3 and want to assign a static IP Address, add these lines to the network interfaces file: `gedit /etc/network/interfaces`
 ```
 auto wlan0
 iface wlan0 inet static
 address 192.168.200.xxx
 netmask 255.255.255.0
 gateway 192.168.200.254
 wpa-ssid "EECSDS3"
 wpa-psk "<check with OIC>"
 dns-nameservers 66.155.216.122 207.59.153.242
```
- If you are connected to EECSnet[(screenshot)](https://github.com/westpoint-robotics/usma_embedded_computer/blob/master/UbuntuEECSNetWirelessConfiguration.jpg) and would like a static IP address, provide your OIC with the IP address (10.113.xx.xx) and we can reserve it for the device.
- Disable automatic updates
 - Go to 'System -> Administration -> Software & Updates -> Updates' and set the following:
 - 'Automatically check for updates: Never'
 - 'When there are security updates: Display Immediately'
 - 'When there are other updates: Display every two weeks'
 
### 5. Install ROS
- Follow instructions on [ROS Wiki](http://wiki.ros.org/kinetic/Installation/Ubuntu) for installing the latest version of ROS i.e. Kinetic Kame. Download the 'full-desktop' version. It is compatible with Ubuntu 15.10 and 16.04 LTS. 
- If you have an older platform such as Ubuntu 14.04 LTS, [ROS Indigo Igloo](http://wiki.ros.org/indigo) is reccommended. [[g-r]](http://www.german-robot.com/2016/05/26/raspberry-pi-sd-card-image/)
- After ROS installation is complete, install additional tools: `sudo apt-get install ant git-core python-argparse python-wstool python-vcstools python-rosinstall python-rosinstall-generator python-rosdep ros-kinetic-control-msgs ros-kinetic-joystick-drivers`
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
### 5. Install Turtlebot2 packages
- `sudo apt-get install ros-kinetic-turtlebot*`
- `sudo apt-get install ros-kinetic-teleop-twist-joy`

### 6. Environment variables for minimal-launch
- Copy and paste the following lines at the bottom of the ~/.bashrc file:
```
export TURTLEBOT_BASE=kobuki
export TURTLEBOT_BATTERY="/sys/class/power_supply/hidpp_battery_2"
export TURTLEBOT_3D_SENSOR=astra
export TURTLEBOT_SIMULATION=false
export TURTLEBOT_SERIAL_PORT=/dev/kobuki
```

### 7. Udev rules for Orbbec Astra RGB-D camera [[1]](http://wiki.ros.org/astra_camera)
- Plug in the camera and let the drivers auto-install
- `gksu gedit /etc/udev/rules.d/56-orbbec.rules`
- Add the lines contained in [this](https://github.com/westpoint-robotics/os-setup/blob/master/orbbec_camera_udev.txt) text file.
- Save and close text editor.
- Unplug the camera, run `sudo service udev reload` and then `sudo service udev restart`.
- Plug the camera back and it should run with the ROS packages now.

### 8. Enable auto-login
- `gksu gedit /usr/share/lightdm/lightdm.conf.d/60-lightdm-gtk-greeter.conf`
- Add this line `autologin-user=odroid` under `[SeatDefaults]`
- Here the username is odroid. Replace if your username if different.
- Restart ntp service:
```
sudo service ntp stop
sudo ntpd -gq
sudo service ntp start
```

--------------------------------------------
### References
#### 1. [Hardkernel FAQs](http://www.hardkernel.com/main/products/prdt_info.php?g_code=G143452239825&tab_idx=3)
#### 2. [Odroid XU4 Wiki](https://wiki.odroid.com/odroid-xu4/odroid-xu4)
#### 3. [eMMC Bootloader Recovery](https://wiki.odroid.com/accessory/emmc/recovery_xu4)
