# AIC8800DC
Linux driver for AICSemi AIC8800DC, ID a69c:88de

## Usage
```bash
# install setup files
chmod +x install_setup.sh
sudo ./install_setup.sh

# if in a virtual machine, execute this command before install driver
# modprobe cfg80211

# build kernel module
cd drivers/aic8800
make
sudo make install

# load kernel modules
sudo modprobe aic8800_fdrv
sudo modprobe aic_load_fw
```
Remember to reboot the system.

## Raspberry PI
The AIC8800DC WIFI usb dongle must be switched from the storage mode to the
WIFI card mode. The following will add a rule to automatically do this for
you at boot time.

```sh
edit the following file

$ sudo nano  /lib/udev/rules.d/40-usb_modeswitch.rules

below the following line

SUBSYSTEM!="usb", ACTION!="add",, GOTO="modeswitch_rules_end"

add two lines

# D-Link DWA-X1850 USB WiFi Adapter , Alfa AWUS036AXER USB WiFi Adapter
ATTR{idVendor}=="a69c", ATTR{idProduct}=="5721", RUN+="usb_modeswitch '/%k'"

save the file ( Ctrl + x, y, Enter )

create the file /usr/share/usb_modeswitch/a69c:5721

$ sudo nano /usr/share/usb_modeswitch/a69c:5721

put the following inside:

#  AIC8800DC USB WiFi Adapter , AIC8800DC USB WiFi Adapter
TargetVendor=0xa69c
TargetProductList="88dc"
StandardEject=1
```
