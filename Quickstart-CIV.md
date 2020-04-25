# Quickstart Guide - CIV Celadon in VM

## Ubuntu Installation
Follow the Quickstart-CIC.md first for instructions on Ubuntu Installation and version

## Download files
All the Celadon VM binaries are stored here: https://github.com/projectceladon/celadon-binary

Go to this link and download all the files: https://github.com/projectceladon/celadon-binary/tree/master/CIV_01.20.01.12_A10

## Setup And Run CIV
```
mkdir -p ~/civ && cd ~/civ
mv <DOWNLOAD FOLDER>/* .
chmod +x *.sh

#Missing from configuration file
sudo apt install -y flex

sudo -E ./setup_host.sh
#Type Y to REPLACE QEMU
#Hit ENTER if asked about "Configuration file '/etc/puls/default.pa'
#Type Y to /etc/default/grub
#Allow the system to reboot if necessary

sudo ./start_flash_usb.sh caas-flashfiles-eng.build.zip

sudo -E ./start_android_qcow2.sh
```




