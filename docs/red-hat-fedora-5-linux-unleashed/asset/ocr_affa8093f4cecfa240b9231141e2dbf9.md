audio CD into .wav file format, with each track saved in a separate file. Other utilities might only need to know the name of the device, such as `/dev/scd1`, like this:

```
```bash
# cdparanoia -d /dev/scd1 -B
cdparanoia 1.11 release 9.8 (March 23, 2001)
(C) 2001 Monty <monty@xiph.org> and Xiphophorous

Report bugs to paranoia@xiph.org
http://www.xiph.org/paranoia/

  Couldn't disable kernel command translation layer
Ripping from sector     0 (track 1 [0:00.00])
   to sector 234821 (track 8 [6:01.04])
```
```

outputting to `track01.cdda.wav`

> **NOTE**
> Fedora also includes the `cdrdao` command, which can create Disk-At-Once (DAO) audio and data CD-ROMs. Other types of CD recording supported by Linux drivers and various CD drives include Track-At-Once and Session-At-Once, which turn the drive's laser on and off during various stages of the recording process.

In this example, the CD-RW device name is used, and, again, all tracks from an audio CD will be extracted and saved as `.wav` audio files. Other graphical clients, such as **xine**, **grip**, and **xcdroast**, are included with Fedora and can be used to create or copy audio and data CDs. See Chapter 10 for more details on burning CDs.

# # Configuring Wireless Networks

Wireless networking used to be a pig to configure for Linux, requiring a lot of complicated steps in order to connect to a wireless network. However, Fedora 5 includes a great utility called NetworkManager that makes connecting to and managing wireless networks extremely easy. Thanks to the inclusion of several wireless chipset drivers in the Fedora Linux kernel, it is now very easy to connect to WEP and WPA encrypted wireless networks.

If you have an Intel Centrino-based system then you need to retrieve the latest firmware from `http://ipw2200.sourceforge.net`, unpack it and copy the contents of the file to `/lib/firmware`. For Broadcom-based wireless systems, you need to retrieve the **fwcutter** program to extract the firmware from the relevant driver file. Head on over to `http://tinyurl.com/ceemyd` for full instructions on where to retrieve the driver files and also how to use **fwcutter**. When you have extracted the firmware, you need to place it in the `/lib/firmware` directory. After you have a set of firmware files in place, you need to activate NetworkManager in `system-config-services` as well as NetworkManager Dispatcher.