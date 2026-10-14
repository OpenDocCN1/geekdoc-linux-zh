All of the Ubuntu files required to run Ubuntu are located on your Windows hard drive in the Ubuntu folder. If you want to remove Ubuntu from your Windows drive, don’t just delete the folder. Go to the Add/Remove Software tool in the Windows Control Panel and select the Ubuntu software to uninstall. Ubuntu will remove all of the files, including the Ubuntu option from the Windows boot menu, restoring your PC to the way it was before Ubuntu was installed.

Although running Ubuntu from your Windows partition is faster than using it on the LiveCD, there’s still a performance penalty. To get the full benefit of Ubuntu, you should install it as a separate partition on a hard drive. That’s exactly what we’ll do in the next chapter.

# Summary

The Ubuntu LiveCD distribution allows you to get a feel for how Ubuntu would run on your PC without having to go through a full installation. This chapter walked through the steps of downloading and creating a LiveCD, then booting and using the LiveCD.

Several versions of the LiveCD are available. The standard Ubuntu workstation installation is available on the desktop-i386 LiveCD image. After downloading the image, you’ll want to verify that the image isn’t corrupted or has been tampered with. Ubuntu uses both MD5 and SHA1 hashes to verify the authenticity and accuracy of the downloaded file. Mac OS X and Linux systems include MD5 hash programs to calculate the hash value of the downloaded image. The winmd5sum program is a free utility you can download for Windows to calculate MD5 hashes.

After explaining how to download and verify the LiveCD ISO image file, the chapter discussed how to burn the image onto a CD. Mac OS X includes a CD-burning utility in the Disk Utilities package. Most Linux distributions include either the K3b or Brasero CD-burning packages. For Windows PCs, some free CD-burning tools don’t provide the option of burning an ISO image file to CD. You can download the InfraRecorder package for free. This package can burn ISO image files to CDs from Windows.

After creating the LiveCD the chapter covered how to boot from it on your PC. Some PCs are configured to automatically detect a CD in the CD tray and boot, while others require a change to the system BIOS settings or hitting a special key at boot time.

Once booted into the Ubuntu LiveCD you’ll be able to run the Ubuntu desktop directly from the CD. This is an excellent way to check out hardware compatibilities before trying to install Ubuntu.

Finally, the chapter discussed the Wubi project. The Wubi project provides an interface within Windows to load Ubuntu as a file on the Windows hard drive partition and boot the file from the Windows boot loader. This enables you to install Ubuntu directly on top of an existing Windows PC without having to repartition the hard drive.

The next chapter walks through the official Ubuntu installation process. This includes installing Ubuntu on an existing Windows PC as a second partition, as well as converting an entire PC into an Ubuntu workstation.