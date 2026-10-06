Android-powered device in Ubuntu is quite simple, and it's only slightly different from working with one of Apple’s “i” devices. Basically, this is the process:

+   1. Connect your Android-powered device to your computer using the USB cable that came with it.

+   2. In the dialogue that appears on your Android device, asking what you want to do now that you are connected to an external device, press the Mass storage button.

+   3. In the next screen that appears on your Android device, press Connect storage to PC.

+   4. The first time you do this, another small window will then appear on your device telling you that some apps might not work when your device is connected as a USB storage device. Click OK.

NOTE Because different versions of the Android system are in service, it is possible that the details of the process described here be slightly different from what you need to do with your phone. You should still be able to follow along.

Similar to what happens in the case of the iPhone, iPod, and iPad, or one more windows will appear asking what you want to do with the photos and music files on your device, and an icon for your device should appear in the side pane of any open file manager and in the Launcher.

To “ject” your device, right-click either the file manager or Launcher icon for the device and then click Eject in the pop-up menu. On your phone, press Disconnect storage from PC.

# What About Kindles, NOOKs, and Android 3.0+ “Honeycomb”-Based Devices?

In the very recent past, getting Kindles or NOOKs or tablets with the newer Android 3.0+ operating system (known as “Honeycomb”) to work with Ubuntu involved a lot of around the command line. The reason was that these devices did not use the USB protocol that most of the other devices in this class use. Instead they used a transfer protocol called MTP (Media Transfer Protocol) which was not Linux (or ever Mac) friendly. The good news is that while these devices still use the MTP file transfer protocol, Linux, as of this Ubuntu 12.04 release, has no problems working with these devices. This means that all connection and file transfer problems are gone, and your device should work with Ubuntu just like all the others mentioned in this chapter.