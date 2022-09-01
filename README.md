== USB Controller Hotplug for Libvirt

This is a repository intended just for my convenience, not a supported open source project. Use at your own risk.

Original hotplug script comes from here: https://github.com/olavmrk/usb-libvirt-hotplug

Copy files in the same directories as stored here.

Update the rules files with the proper PCI paths. To find out, run this command:

`udevadm monitor --property --udev --subsystem-match=usb/usb_device`

It will output something similar to this:

`UDEV  [99053.325971] bind     /devices/pci0000:00/0000:00:01.2/0000:02:00.0/0000:03:08.0/0000:09:00.1/usb3/3-3/3-3.3/3-3.3.1/3-3.3.1.2 (usb)
ACTION=bind
DEVPATH=/devices/pci0000:00/0000:00:01.2/0000:02:00.0/0000:03:08.0/0000:09:00.1/usb3/3-3/3-3.3/3-3.3.1/3-3.3.1.2
SUBSYSTEM=usb
DEVNAME=/dev/bus/usb/003/017
DEVTYPE=usb_device
DRIVER=usb
PRODUCT=45e/b12/50d
TYPE=255/71/208
BUSNUM=003
DEVNUM=017
SEQNUM=32882
USEC_INITIALIZED=99053201501
ID_VENDOR=Microsoft
ID_VENDOR_ENC=Microsoft
ID_VENDOR_ID=045e
ID_MODEL=Controller
ID_MODEL_ENC=Controller
ID_MODEL_ID=0b12
ID_REVISION=050d
ID_SERIAL=Microsoft_Controller_3039373130393437393334313131
ID_SERIAL_SHORT=3039373130393437393334313131
ID_BUS=usb
ID_USB_INTERFACES=:ff47d0:
ID_VENDOR_FROM_DATABASE=Microsoft Corp.
ID_MODEL_FROM_DATABASE=Xbox Wireless Controller (model 1914)
ID_PATH=pci-0000:09:00.1-usb-0:3.3.1.2
ID_PATH_TAG=pci-0000_09_00_1-usb-0_3_3_1_2
MAJOR=189
MINOR=272`


Just copy the DEVPATH value as shown above in the rules files. Then restart udevd:

`sudo systemctl restart systemd-udevd`
