# 9.3 Using rsync

# 9.3.1 Introduction

The rsync program is a fast and flexible tool for remote backup. It is common on UNIX and UNIX-like systems, easy to configure and use in scripts. While the r in rsync stands for "remote", you do not need to take this all too literally. Your "remote" device might just as well be a USB storage device or another partition on your hard disk, you do not need to have two separated machines.

# 9.3.2 An example: rsync to a USB storage device

As discussed in Section 3.1.2.3, we will first have to mount the device. Possibly, this should be done as root:

```
root@theserver# mkdir /mnt/usbstore
```

```
root@theserver# mount -t vfat /dev/sda1 /mnt/usbstore
```

# Userfriendly

More and more distributions give access to removable devices for non-privileged users and mount USB devices, CD-ROMs and such automatically.

Note that this guideline requires USB support to be installed on your system. See the USB Guide <http://www.linux-usb.org/USB-guide/> for help if this does not work. Check with dmesg that /dev/sda1 is indeed the device to mount.

Then you can start the actual backup, for instance of the /home/karl directory:

```
karl@theserver:-> rsync -avg /home/karl /mnt/usbstore
```

As usual, refer to the man pages for more.

# 9.4 Encryption

# 9.4.1 General remarks

# 9.4.1.1 Why should you encrypt data?

Encryption is synonym to secrecy. In the context of backups, encryption can be very useful, for instance if you need to leave your backed up data in a place where you can not control access, such as the server of your provider.

Apart from that, encryption can be applied to E-mails as well: normally, mail is not encrypted and it is often sent in the open over the network or the Internet. If your message contains sensitive information, better encrypt it.