Since these images are available, your task of installing Kali on an ARM device is greatly simplified. Here are the basic steps:

+   1. Download the image for your ARM device and ensure that the checksum matches the one provided on the website (see 2.1.3, "Verifying Integrity and Authenticity") [page 16] for explanations on how to do it). Note that the images are usually xz-compressed; make sure to uncomment with unxz.

+   2. Depending on the storage expansion slot available on your specific ARM device, acquire an SD card, micro card, or eMMC module that has a capacity of 8 GB.

+   3. Copy the downloaded image to the storage device with dd. This is similar to the process of copying an ISO image onto a USB key (see 2.1.4, "Copying the Image on a DVD-ROM or USB Key") [page 19].

```
# dd if=kali-image.img of=/dev/sd=512k
```

+   4. Plug the SD-card/eMMC into your ARM device.

+   5. Boot your ARM device and log into it ("root" or "toor"). If you don't have a screen connected, you will have to figure out the IP address that has been assigned by DHCP and connect to address over SSH. Some DHCP servers have tools or web interfaces show the current leases. If you don't have anything like that, use a sniffer for DHCP lease traffic.

+   6. Change the root password and generate new SSH host keys, especially if the device will be permanently running on a public network! The steps are relatively straightforward, see "Generating New SSH Keys") [page 111].

+   7. Enjoy your new ARM device running Kali Linux!

| Special Cases and More Detailed Documentation | These instructions are generic and while they work for most devices, there are always exceptions. For example, Chromebooks require developer mode and other devices require a special keypress in order to boot from external media. 
 Since ARM devices are added relatively frequently and their specifications are dynamic, we won't cover specific installation instructions for ARM devices here. Instead, refer to the dedicated "Kali on ARM" section of the Kali documentation website for information about each ARM device supported by Offensive Security: 
 >> http://docs.kali.org/category/kali-on-arm |

# 4.5. Troubleshooting Installations

The installer is quite reliable, but you may encounter bugs or face external problems such as: network-problems, bad mirrors, and insufficient disk space. Because of this, it quite useful to be able to troubleshoot problems that appear in the installation process.