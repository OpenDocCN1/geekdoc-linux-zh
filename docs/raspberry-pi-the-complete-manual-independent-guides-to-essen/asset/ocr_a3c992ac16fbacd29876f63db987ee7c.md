# Install a distro

# Getting started

# Obtaining OSs

01 One of your first questions may be 'where can I find some operating systems to download?'

Most of the common images can be found on the main Raspberry Pi site: *http://www.raspberrypi.org*/ *downloads*. These are stable and well tested systems worth investigating.

# Unzipping

02 When you've downloaded your image, the first thing you'll most likely need to do is unzip it. This can be done in Windows by right clicking and choosing 'extract...'. In OS X, just double click to extract the files.

# OS Format

03 Within the zip you'll find a file with a .img or .iso extension. These are the equivalent of a 'snapshot' of an installation CD or DVD. Simply copying the file to the SD card won't do anything, you'll need to use a program to extract it.

# SD card format

04 The SD card that you'll boot to make sure there is nothing important on it first. You'll also need to format it to use the FAT32 file system. This is a common system, used by most USB sticks and cameras.

# Formatting the card

05 In Windows, to format the card simply insert and wait for it to mount. Then click on 'My Computer' and then right click on the cards icon. After that choose format and then 'FAT32' from the drop-down menu.

# Using the terminal

06 If you are using OS X or Linux, then you'll have to use the terminal to copy the image. In OS X, the Terminal app comes installed by default, and most Linux versions come with one in some form or other. It may be referred to as the 'console' or 'command line'.

# DD command

07 The command you need to use is called *dd*. This is entirely in the format of sudo dd bs=1m <file>| <device>|. An example of this can be seen below:

```
sudo dd bs=32m if=/Users/rachel1crab/Desktop/archlinux/armchlinux-hf-2013-02-11.img of=/dev/disk1
```

# Win 32 Disk Imager

08 Windows users can use Win32 Disk Imager. Once you've downloaded the tool, simply right click on the *.exe*, and choose 'run as administrator' and follow the prompts. When the installation is complete you can put the SD card in your Pi. Easy!