# Quickstart Guide - CIV Celadon in VM

## Download files
All the Celadon VM binaries are stored here: https://github.com/projectceladon/celadon-binary
```
mkdir ~/civ
cd ~/civ
wget https://github.com/projectceladon/celadon-binary/raw/master/CIV_01.20.01.12_A10/caas-flashfiles-eng.build.zip

wget https://raw.githubusercontent.com/projectceladon/device-androidia-mixins/master/groups/device-specific/caas/start_flash_usb.sh
wget https://raw.githubusercontent.com/projectceladon/device-androidia-mixins/master/groups/device-specific/caas/auto_switch_pt_usb_vms.sh
wget https://raw.githubusercontent.com/projectceladon/device-androidia-mixins/master/groups/device-specific/caas/findall.py

chmod +x *.sh *.py
```

## Setup And Run CIV
```
sudo ./start_flash_usb.sh caas-flashfiles-eng.build.zip --display-off
sudo -E ./start_android_qcow2.sh
```
## Troubleshooting
### Nested VT Error
If you receive an error complaining about nested vt, enable it with these commands
```
sudo modprobe -r kvm_intel
sudo modprobe kvm_intel nested=1
```
