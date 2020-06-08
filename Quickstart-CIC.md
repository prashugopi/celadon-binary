# Quickstart - CIC/AIC Android/Celadon in a Container

## Install Ubuntu - Validated with 18.04.4 Desktop

Download ISO from: https://ubuntu.com/download/desktop

Burn onto USB drive (we use https://rufus.ie/ )

Reboot, boot to USB and install Ubuntu
* Minimal Installation

## Download CIC Binary
All the prebuilt images can be found here: https://github.com/projectceladon/celadon-binary/
We’ll be using https://github.com/projectceladon/celadon-binary/tree/master/CIC_00.19.04.20.03_A09

## Run installation scripts
```
mkdir ~/cic
cd ~/cic
cp <FROM DOWNLOADS>/cic_dev-aic-CC0000059.tar.gz .
tar xvzf cic_dev-aic-CC0000059.tar.gz
 
## Install Docker
sudo su
apt-get update
apt install -y curl
cd pre-requisites
./install-docker
cd ..
 
./setup-aic
#Hit ENTER to reboot
```
## Run CIC (X11 mode - Recommended for development) 
```
echo $DISPLAY
#Make sure output is :0 
#If not see section below
 
#x11 is default
sudo su
cd ~/cic
./aic install -d x11
./aic start
 
#When done
./aic stop
```
## Troubleshooting X11 Issues
Does the command echo $DISPLAY result in :1? 
Does the command ps aux | grep Xorg result in a gdm and a $USER instance?

Install lightdm using this command: sudo apt-get -y install slick-greeter 
Click on lightdm when prompted.

## Pass through of USB device 
```
#Find the device to pass through manually
cat /proc/bus/input/devices
#For example, for USB devices specifically
cat /proc/bus/input/devices | grep "usb" -B 3 -A 6

#Look for the line like this that matches your device:
Sysfs=/devices/pci0000:00/0000:00:14.0/usb1/1-2/1-2.4/1-2.4:1.0/0003:0404:0210.0013/input/input41

#Capture the bold portion of the line
/pci0000:00/0000:00:14.0/usb1/1-2/1-2.4/1-2.4:1.0/0003:0404:0210.0013/input/input41

#Add any lines to the file:
./workdir/ipc/config/input/input0 

#Backup the file
cp ./workdir/ipc/config/input/input0 input0

#Create the container with the -m option
./aic install -m
```

## Run CIC (DRM mode - Recommend for deployment) 
Booting into DRM will take over the whole screen, including USB devices. You will need to hard reset the machine, or you will need SSH access in order to start (and more importantly stop) the containers.

Hit ALT+CTRL+F1/F2/F3/FX → one of these combinations will switch you text mode (black/white) just text, no GUI

```
#AS ROOT
cd ~/cic
./aic install -m -d drm
./aic start
 
#When done
./aic stop
```

## ADB debugger / Installation of APK
```
#Install and start adb server
#AS ROOT
apt-get install -y adb
 
#start aic instance
./aic start
 
#Start adb server
adb devices
 
#Install APK file
#Download any APK file for installation
adb -s emulator-5554 install /path/to/file.apk
 
#App files are downloaded to folder:
# workdir/data0/app/*
```
 

## Troubleshoot: Unable to see any devices when adb devices is ran
```
#restart server
sudo adb kill-server
sudo adb start-server
```

## Portainer
#Install and start portainer
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
 
#Open web browser to 127.0.0.1:9000


