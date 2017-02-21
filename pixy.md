#### Instructions to use Pixy Cam and Pixy Mon on a Linux computer

### Pixy Cam
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

4. Set signature using the button on Pixy 
 - [Instructions](http://cmucam.org/projects/cmucam5/wiki/Teach_Pixy_an_object_2#Teach-Pixy-an-Object)
 - [Video Demo] (https://www.youtube.com/watch?v=7znEmgYZXL0)
 
5. Build and Run example script
 - `./build_hello_pixy.sh`
 - `cd ../build/hello_pixy`
 - `sudo ./hello_pixy`
 - In the output, you should see block information if color signatures have been set and if the signatures are currently being detected by Pixy.
 
6. Install PixyMon (Optional) [[1]] (http://cmucam.org/projects/cmucam5/wiki/Installing_PixyMon_on_Linux)
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
  - [Instructions](http://cmucam.org/projects/cmucam5/wiki/Teach_Pixy_an_object_2#Teaching-through-PixyMon) to train the PixyCam through PixyMon
  ---------------------------------------------------------
  
  - [Update Pixy Firmware] (http://cmucam.org/projects/cmucam5/wiki/Uploading_New_Firmware)
  - 
