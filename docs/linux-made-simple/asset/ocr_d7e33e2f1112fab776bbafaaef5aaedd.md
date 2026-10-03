# Networking

How your computer talks to others.

![](bbox=[0.66, 0.08, 0.92, 0.35])

Networking is core to Linux. Even on a standalone machine with no connection to a local network, let alone the internet, networking is still used. Many services run on a client/server model, where the server runs in the background waiting for instructions from other programs. Even something as basic as the system logger runs as a networked service, allowing other programs to write to log files. The X graphics system is also networked, with the X server running the desktop and programs, telling it what they want displayed. This is why it is so simple to run X programs on a remote desktop – as far as the system is concerned, there is no major difference between that and opening a window locally.

Running ifconfig will always show at least one interface, called lo with an address of 127.0.0.1 – this is used by the computer for talking to itself, which is regarded as a more sane activity for computers than people. Most other networking is based on TCP/IP, either over wired Ethernet or wireless, but there are other types of network in use. All distros and desktops include good tools for configuring and maintaining TCP/IP networks, from the fairly ubiquitous NetworkManager to individual tools such as Gnome’s network configuration tool or OpenSUSE’s YaST. More recent

additions to the networking scene include 3G mobile communications and PAN (Personal Area Network) technologies such as Bluetooth. Using a 3G mobile broadband dongle is usually simple, either using NetworkManager or your desktop’s PPP software. Yes, 3G modems really do work like modems using dials and everything, but without the cacophony of squawks as you connect (younger readers should ignore the last statement). Most problems with 3G are caused by trying to set them up in a poor signal area rather than with either the hardware or software support in Linux.

# The protocol of kings

Bluetooth is becoming more important as mobile devices proliferate, and the number of input and output devices using it is increasing. It’s not only phone and tablet users who benefit – a Bluetooth mouse and speakers can enhance the use of a laptop when at your desk, without having to plug everything in before you can start working. PulseAudio (see the section on sound) makes this easier, because it can switch between devices when they are detected.

# Storage

Storing data on a hard disk can involve several layers in itself. All physical storage (as opposed to network storage) in Linux revolves around block devices, so called because disks store data in blocks. A block device like /dev/sda1 does indeed refer to blocks, physical areas on the disk, and a collection of them as a disk partition. On top of that we have a filesystem, which is how the data is stored in a sensible structure of directories and files, containing both data and metadata.

What’s the difference? Let’s say you save a file containing some text. The data in that file is the text, but the file has other attributes: there is the owner of the file, the time they created it, the time they last modified it, the time it was last read and who has permission to read or modify it. This is the information you see when you ls -l a file, or inspect its properties in your file manager, and this is stored by the filesystem. The standard filesystem in use nowadays is ext4, but there are alternatives such as ext3, ReiserFS, XFS, JFS and, of course, FAT and NTFS from the world of Windows.

![](bbox=[0.42, 0.52, 0.86, 0.76])

Networking is core to the operation of a Linux system. The localhost interface is set up automatically; for the rest we have programs such as NetworkManager.

# Other Linuxes

Everything we have covered relates to Linux running on desktops, laptops and servers – traditional computer hardware if you like, but there are other environments where Linux is used. Many embedded devices, from routers to PVRs and set-top boxes, run Linux, and in many ways it’s similar to the Linux we know and love. If

your router allows SSH access, you will often feel at home as soon as you log in.

There is another class of device that has seen a huge uptake in recent years and runs a rather different Linux. No prizes for guessing we are referring to the smartphone and its tablet siblings, running Android. Android is Linux, it uses

a Linux kernel, but it is not GNU/Linux. The kernel may be based on the same source code, but everything running on top is different. The principles are similar in some ways, but the implementation is very different – although you will find familiar command line tools if you can get to a shell prompt on your phone.