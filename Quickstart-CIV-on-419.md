# Quickstart Guide - CIV Celadon in VM

## Download files
All the Celadon VM binaries are stored here: https://github.com/projectceladon/celadon-binary
```
mkdir ~/civ
cd ~/civ
wget https://github.com/projectceladon/celadon-binary/raw/master/CIV_01.20.01.12_A10/caas-flashfiles-eng.build.zip

```

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
#To install qemu
sudo apt install -y libaio-dev libsdl2-dev libspice-server-dev 
#Windows specific
sudo apt install -y samba

sudo modprobe -r kvm_intel
sudo modprobe kvm_intel nested=1

#Minimum CIV
	wget https://raw.githubusercontent.com/projectceladon/device-androidia-mixins/master/groups/device-specific/caas/start_flash_usb.sh
    wget https://raw.githubusercontent.com/projectceladon/device-androidia-mixins/master/groups/device-specific/caas/start_android_qcow2.sh
    wget https://raw.githubusercontent.com/projectceladon/device-androidia-mixins/master/groups/device-specific/caas/auto_switch_pt_usb_vms.sh
    wget https://raw.githubusercontent.com/projectceladon/device-androidia-mixins/master/groups/device-specific/caas/findall.py
    chmod +x auto_switch_pt_usb_vms.sh
    chmod +x findall.py
    chmod +x start_flash_usb.sh
    chmod +x start_android_qcow2.sh
	sudo modprobe 9pnet
    sudo modprobe 9pnet_virtio
    sudo modprobe 9p

sudo ./start_flash_usb.sh caas-flashfiles-eng.build.zip --display-off



