# Graphics, Multimedia, and Productivity Tools
PART IV

information on the extended functionality. Some of the upgraded features may not be included with the SuSE 6.2 distribution (see the OSS software license agreement for further information).

# Advanced Linux Sound Architecture (ALSA)

ALSA is an alternative to the OSS/Lite and the commercial sound drivers from 4Front Technologies. It contains some advanced features and started out from the Linux Ultra Sound Project. The ALSA-project Web page ( http://www.alsa-project.org) indicates that the following are primary goals:

+   * Create a fully modularized sound driver that supports kernel and kmod.
* Create the ALSA Kernel API, which surpassed the current OSS API.
* Maintain compatibility with most OSS/Lite binaries.
* Create the ALSA Library (C, C++), which simplifies ALSA application development.
* Create the ALSA Manager, an interactive configuration program for the driver.

ALSA-sound mini-HOWTO, created by Valentijn Sessink, version 1.7, dated July 29, 1999, is a good source of information on installation of the ALSA drivers.

The ALSA drivers are available from the SuSE 6.2 CD-ROM and can be loaded using YaST under the snd series. The ASLA package, 0.3.0_pre5_1999_03_28_16, is 1.8MB uncompressed. If you have to download or update the drivers, you may be required to compile the modules. This is done just as other items are compiled: follow the ./configure, make, and make install steps as outlined in the documentation.

Using the example of an Ensoniq AudioPCI ES1371, the command would be

```
# /sbin/modprobe snd-audiopci
```

As in the kernel drivers, the sound card can be loaded by the modprobe command, and you can modify the /etc/conf.modules file to load the drivers at startup.

# Playing Audio CDs

There are two ways to listen to music CDs: through the jack on the CD-ROM drive itself and through the sound card. Either way provides an enjoyable experience while working on the PC. The following section describes how to play audio CDs through the sound card your system.