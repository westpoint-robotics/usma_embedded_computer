## Raspberry Pi 3 

### 1. Installing OS (Ubuntu MATE)
 *Our disk is going to be a microSDHC Card. Use one with memory greater than 8GB and speed class higher than 10. [[1]](https://ubuntu-mate.org/raspberry-pi/) [[2]](https://www.youtube.com/watch?v=m5QXsKSwt-c)*
 
#### *To create the OS Disk using a Windows machine:*
 - Your SD Card, if not brand new, may have sector errors and odd partions. It is always advisable to format the drive before laying down the OS. You may download and use [this](https://www.sdcard.org/downloads/formatter_4/) tool.  
 - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.1 LTS for Raspberry Pi.
 - Once download is complete, the .xz file size should be about 1.1GB. Use [7-Zip](http://www.7-zip.org/) or [WinZip](http://www.winzip.com/win/en/downwz.html) to extract the image.
 - Use [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/) to write the image onto the SD card.
 - Open Disk Imager and select path to the image you extracted in the above step. Also select the target device to write onto. This would be the drive corresponding to the SD Card reader (Example- F: or H:)
 
#### *To create the OS Disk using a Linux machine:*
- *Option 1*: Using the 'dd' utility in command line:
  - `sudo apt-get install gddrescue xz-utils`
  - [Download](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz) Ubuntu MATE 16.04.1 LTS for Raspberry Pi. Once download is complete, the .xz file size should be about 1.1GB.
  - `cd Downloads/`
  - `unxz ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img.xz`
  - The microSDHC Card maybe present as /sd**a** or /sd**b**. You can identify the device name by `ls /dev/sd*`
  - Once you've identified 'x' in /dev/sd**x**, run the following command by replacing 'x'.
  - `sudo ddrescue -D --force ubuntu-mate-16.04-desktop-armhf-raspberry-pi.img /dev/sdx`
  - [Here's](https://asciinema.org/a/34243) the complete recording of the terminal while executing these commands
  
- *Option 2*: Using a graphical tool:
  - `sudo apt-get install gnome-disk-utility`
  - After installation is complete, open the GUI and follow [these](https://www.youtube.com/watch?v=V_6GNyL6Dac) steps on using the GNOME Disk utility to 'Restore Disk Image'
 
#### *To Clone from another SD Card:* 
 - [Steps](http://askubuntu.com/questions/227924/sd-card-cloning-using-the-dd-command) to clone an image already installed on another fully-operational SD Card.
 - If you have only a single SD Card reader/slot on your PC, follow [these](http://askubuntu.com/questions/753977/cloning-an-sd-card-to-another-in-ubuntu-using-a-single-sd-card-reader) instructions.

### 2. Initial setup 
- If this your first time with the RPi, you may find the first two pages of this [Quick Start Guide](https://www.raspberrypi.org/qsg) useful. Ignore the SD Card setup portion, we are not utilizing NOOBS.
- On the first boot, the Pi will run through a setup wizard where you can create a user account. Please check with the OIC or Engineering Support Group personnel before creating the username and password. We follow a standard convention for ease of operation.
- The Wireless MAC Address of your device should be registered with the Computer Support Group to be able to connect to the EECSDS3 WiFi. This step is performed for devices issued in class or lab. If you have problems connecting, check with your OIC.

### 3. Install useful software and utilities
- Type the following in a Terminal (Ctrl + Alt + T)
 - Install GNOME text editor: `sudo apt-get install gedit`
 - Install build essential: `sudo apt-get install build-essential -y`
 - Install SSH server: `sudo apt-get install openssh-server`
 - Install modem program: `sudo apt-get install minicom`
 - Install git commands: `sudo apt-get install git`
 
### 4. System Settings
- Assign a Static IP Address on the DS3
 - In a terminal, type `gedit /etc/network/interfaces`. Add these lines:
 - `auto wlan0`
 - `iface wlan0 inet static`
 - `address 192.168.200.xxx` Check with OIC to fill in the last octet.
 - `netmask 255.255.255.0`
 - `gateway 192.168.200.254`
 - `wpa-ssid "EECSDS3"`
 - `wpa-psk "accessgranted"`
 - `dns-nameservers 66.155.216.122 207.59.153.242`
- Disable bluetooth on start-up
 - `gksu gedit /etc/rc.local`
 - Add `rfkill block bluetooth` in the line preceeding `exit 0`.
- Disable automatic updates
 - Go to 'System -> Administration -> Software & Updates -> Updates' and set the following:
 - 'Automatically check for updates: Never'
 - 'When there are security updates: Display Immediately'
 - 'When there are other updates: Display every two weeks'
 
### 5. Install ROS (Optional)
- Follow instructions on [ROS Wiki](http://wiki.ros.org/kinetic/Installation/Ubuntu) for installing the latest version of ROS i.e. Kinetic Kame. It is compatible with Ubuntu 15.10 and 16.04 LTS. 
- If you have an older platform such as Ubuntu 14.04 LTS, [ROS Indigo Igloo](http://wiki.ros.org/indigo) is reccommended. [[g-r]](http://www.german-robot.com/2016/05/26/raspberry-pi-sd-card-image/)
