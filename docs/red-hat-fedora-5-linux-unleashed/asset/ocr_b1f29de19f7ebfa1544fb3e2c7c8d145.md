Webcams can be used to send almost-live images to an online correspondent; many people include screen grabs of themselves at their computer workstations just because they can.

# COFFEE POT CAM

One of the more interesting uses of a webcam was the legendary "Internet coffee pot" cam (turned on 1991, but turned off on August 22, 2001— a day that will live in infamy). A webcam was trained on a coffee maker, and the sysadmin could see whether fresh coffee was available without leaving his cubicle. Some webcams take grabs of intersections in various cities. You are likely to find some similar worthwhile use for your webcam.

You can use any of the video applications that can access a video4linux device to view webcam or still camera images in Fedora. You also can use GnomeMeeting (discussed in Chapter 8, "On the Internet: Surfing the Web, Writing Email, and Reading the News") as a viewer for your webcam.

Not all webcams are supported in Linux and the drivers are based on the chipset used, rather than the model or manufacturer. Some of the files in /usr/src/linux-2.6/ Documentation/usb contain information about USB webcams and drivers supported by Fedora, including

+   • i00amc.txt
+   
+   • dv511.txt
+   
+   • ghillies.txt
+   
+   • sa401.txt
+   
+   • stv0600.txt

Documentation on parallel port cameras, including the CQ Cam (GQcam.txt) and CPlA camera (README-cpia), is found in /usr/src/linux-2.6/Documentation/video4linux/ if you have installed the kernel documentation on your computer.

# TIP

Unfortunately, most of the documentation provided for webcams is abysmal, and it is difficult to associate the webcam you just purchased with a related driver. If you are interested in a particular USB webcam, but are not sure whether it is supported by Linux, browse to http://www.qbik.ch/usb/devices/showdevcat.php?id=9.

# Handheld Digital Cameras

Digital cameras are one of the major success stories of the last few years. Now you can take pictures and see previews of your pictures immediately. The pictures themselves are stored on discs or memory cards that can be easily plugged into Fedora for further manipulation using The GIMP or other software. Unfortunately, most of the supplied software