# Inkscape EggDuino Extension

This Inkscape extension helps you to use the EggDuino based EggBot
from inside Inkscape.

## Installation Linux and OSX
You have to put these two directories inside your ```~/.config/inkscape``` folder.

```bash
git clone https://github.com/justinotherguy/eggbot_extension.git
# If you want a specific branch:
#cd eggbot_extension && git checkout BRANCH && cd ..
mkdir -p ~/.config/inkscape
cp -r eggbot_extension/templates ~/.config/inkscape
cp -r eggbot_extension/extensions ~/.config/inkscape
```

### Dependencies

- Inkscape >= 1.0 (obviously)
- python3
- python-serial

On Debian or Debian-based distributions (Ubuntu, Mint) use apt-get/aptitude/apt, for example
```
sudo apt-get install inkscape python python-serial
```
### Access Rights

On most GNU/Linux distributions you have to be member of a certain group to use serial ports.

On Debian/Ubuntu/Mint this is the `dialout` group to which you can add yourself with
```
sudo addgroup $USER dialout
```

On Archlinux it is the `uucp` group to which you can add yourself with
```
sudo usermod -aG uucp $USER
```

You need to logout/logon or reboot to activate the change.

### Troubleshooting

You aren't able to connect to your EggDuino? Try this:

Disconnect your board from your PC and execute
```
sudo dmesg -w
```
and plugin your Board. You should see something like
```
[ 4285.923992] usb 3-6: new full-speed USB device number 8 using xhci_hcd
[ 4286.065120] usb 3-6: New USB device found, idVendor=1a86, idProduct=7523
[ 4286.065123] usb 3-6: New USB device strings: Mfr=0, Product=2, SerialNumber=0
[ 4286.065124] usb 3-6: Product: USB2.0-Serial
[ 4286.065746] ch341 3-6:1.0: ch341-uart converter detected
[ 4286.066380] usb 3-6: ch341-uart converter now attached to ttyUSB0
```

The important pieces you can extract from the above: Your arduino clone (ch341-uart converter)
is now available as `/dev/ttyUSB0`. You can now check the rights which are needed to access this device:

```
$ ls -la /dev/ttyUSB0
crw-rw---- 1 root dialout 188, 0 Mär  6 08:59 /dev/ttyUSB0
```

So you need to be root or are member of the group `dialout`. Are we?
```
$ groups
dialout cdrom floppy sudo audio dip video plugdev netdev lpadmin scanner bluetooth libvirt sbuild libvirt-qemu
```

Be sure the output of `groups` includes the group `dialout` as it does above.

Then start inkscape, select Erweiterungen/Extensions - EggBot - EggBot Control. On the `Manual` tab you can check the
individual commands like pen up/down.

## Installation Windows
You have to unpack the zip file from https://github.com/section77/eggbot_extension/archive/1.1.zip
and copy the templates and extensions folders to the inkscape/share folder which
is typically located at C:\programme\inkscape\share



## Other Projects Parts

 * [Eggduino Firmware](https://github.com/section77/EggDuino)
 * [Eggbot77 Wiki](https://wiki.section77.de/projekte/eggbot77) (in german)
