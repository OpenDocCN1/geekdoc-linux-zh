
![](img/1744bde8c889adfab3fc911e1687fecf_331_0.png)

**Figure 8-9:** Play music videos, sports, and news from the Web with RealPlayer.

After you have RealPlayer, you can visit some sites to get content to play on your RealPlayer. I suggest starting at the RealGuide site (`realguide.real.com`). This is a guide to audio and video on the Internet that plays on RealPlayers. The guide has links to radio shows and events that are live at the moment. There are also special news reports and links to music, show business, sports, science/technical, society, money, and shopping sites that use this technology.

## Using a Digital Camera with gPhoto

With the gPhoto window, you can download images from digital cameras. gPhoto works by attaching one of the supported digital cameras to a serial port on your computer. You can view an index of thumbnails of the digital images from the camera, view full-size digital images, and download the ones you select from the camera to your Linux system.

Check the gPhoto Web site (`www.gphoto.org`) for information on supported cameras as well as other topics related to gPhoto. Here is a list of digital cameras that are currently supported.

- **Agfa ePhoto** — Supported models: 307, 708, 708C, 1280, and 1680.
- **Apple QuickTake** — Supported models: 150 and 200.
- **Canon Digital** — Supported models: IXUS, IXUS 300 and IXUS v.
- **Canon PowerShot** — Supported models: A5, A5 Zoom, A10, A20, A50, A70, G1, G2, Pro70, Pro90 IS, S10, S100, S110, S300 and S20.
- **Casio QV** — Supported models: 10, 10A, 11, 30, 70, 100, 200, 700, and 5000SX.
- **Chinon** — Supported model: ES-1000.
- **Epson PhotoPC** — Supported models: 500, 550, 600, 700, and 800.
- **Fuji** — Supported models: DS-7, DX-5, DX-10, MX-500, MX-600, MX-700, MX-1200, and MX 2700.
- **Hewlett-Packard PhotoSmart** — Supported models: 618, C20, C30, and C2000.
- **Kodak DC** — Supported models: 120, 20, 25, 200+, 210, 210+ Zoom, 215 Zoom, 220, 240, 260, 265, 280, 290, 3200, 3400, and 5000.
- **Konica** — Supported models: QM100, QM100V, Q-EZ, Q-M100, Q-M100V, and Q-M200.
- **Leica** — Supported model: Digilux Zoom.
- **Minolta** — Supported model: DiMage V.
- **Mustek** — Supported model: MDC 800 v2.
- **Nikon CoolPix** — Supported models: 100, 300, 600, 700, 800, 880, 900, 900S, 910, 950, 950S, and 990.
- **Olympus** — Supported models: D-100Z, D-200L, D-220L, D-300L, D-320L, D-330R, D-340L, D-340R, D-400L Zoom, D-450Z, D-500L, D-600L, D-620L, C-400L, C-410L, C-800L, C-820L, C-830L, C-840L, C-900 Zoom, C-900L Zoom, C-1000L, C-1400L, and C-2000Z.
- **Panasonic** — Supported models: Coolshot KXL-600A and KXL-601A, and NV-DCF5E, and DC1000 and DC1580.
- **Philips** — Supported models: ESP60 and ESP 80.
- **Polaroid** — Supported models: PDC 640 and DC700.
- **Ricoh RDC** — Supported models: 300, 300Z, 4200, 4300, and 5000.
- **Samsung** — Supported models: Kenox SSC-350N and Digimax 800K.
- **Sanyo VPC** — Supported models: G210, G200, G200EX, G250, X300, and X350.
- **Sony** — Supported models: DSC-F1, DSC-F55, DSC-F505, Memory Stick Adapter, and MSAC-SR1 and DCR-PC100.
- **Toshiba** — Supported model: PDR-M1.

To start gPhoto from the Gnome desktop menu, choose Programs → Multimedia → gPhoto. A pop-up window asks you to identify the type of camera you are using and the port that it is connected to. Make sure that your camera is set to send and receive data. At this point you should have your camera attached to a serial port (such as COM1 or COM2) on your computer. After identifying your camera and port, click Save. The main gPhoto window appears, as shown in Figure 8-10.

![](img/1744bde8c889adfab3fc911e1687fecf_333_0.png)

**Figure 8-10:** Download images from digital cameras from the gPhoto window.

To view images from your digital camera, choose Camera → Download Index. Then either select Thumbnails (to display thumbnail views of each image) or No Thumbnails to simply see a gray box representing each image. Thumbnails take much longer to appear than the gray boxes. So if you want to just select one image at a time to view, you can click No Thumbnails.

After images are selected, choose Camera → Download Selected → Thumbnails. Then select either Images or Thumbnails. After that, you can select either Open in window (to view the selected images) or Save to disk (to save the selected images).

After images are displayed, you can rotate the images, flip them vertically or horizontally, resize them, or modify colors. You can also save, print, or delete selected images.

> **TIP:** If the digital camera you have is not supported, you might need to use the gphoto2 interface. Although gphoto2 is a command-line interface, you can use gphoto2-supported cameras with other GUI front ends. One such front end is gtKam (Programs → Graphics → gtKam).

## Multimedia Netscape Plug-ins and Helper Apps

Because much of your stock of video clips, audio clips, and other multimedia content will probably come from the Internet, it makes sense to be able to play that content in your Internet browser. Software added to Netscape Navigator to play different content takes the form of plug-ins and helper apps.

In simple terms, a Netscape plug-in is software that plays a particular type of data (a video, sound clip, or other form of content) within the Netscape display area. A helper app is software that is launched as a separate application by Netscape to handle a particular type of data (usually by opening a separate window).

Compared to the number of plug-ins available for the Windows platforms, very few plug-ins can be used with your Red Hat Linux system. Those plug-ins that apply to multimedia content are described in the text that follows. Any application that can play multimedia content in Red Hat Linux, however, can be added to Netscape as a helper application. See Chapter 9 for a description of how to add helper applications to Netscape.

Here are two plug-ins for Netscape that come with Red Hat Linux and allow you to play some types of multimedia content that you may not otherwise be able to play in Linux.

- **Shockwave Flash Player** — This plug-in plays multimedia FutureSplash content created by Flash 3 authoring software from Macromedia (www.macromedia.com). It also plays Shockwave Flash multimedia content. Flash content can contain animation, vector graphics, sound, and interactive interfaces.
- **Plugger** — This is a streaming multimedia plug-in for Netscape on UNIX platforms. On the back end of Plugger are applications such as Xanim, MpegTV, and several other applications that actually process the data. (In other words, these other applications need to be installed so that Plugger can use them to provide the features you select.)

Another plug-in you should consider installing is the Adobe Acrobat Reader plug-in. You can get it by installing the acroread. (You can use the rpmfind acroread command to locate a copy of the acroread package from the Internet.)

Installing a plug-in often means simply copying the plug-in file to the directory where Netscape will find it. On my system the location is the /usr/lib/netscape/plugins directory. The best way to find this location, as well as a list of other plug-ins that are already installed, is to open Netscape and then choose Help → About Plug-ins. Figure 8-11 shows what this listing looks like after I installed the Adobe Acrobat Reader plug-in.

![](img/1744bde8c889adfab3fc911e1687fecf_334_0.png)

Figure 8-11: Find what plug-ins are installed in Netscape using Help → About Plug-ins.

The listing of plug-ins shows the name of the plug-in, the MIME type of the content it can play, and the filename extensions on the files it can play.

## Recording Music CDs

Writable CD-ROM drives are fast becoming a standard device on computers. Where once you had to settle for a floppy disk (1.44MB) or a Zip disk (100MB) to store personal data, a CD-ROM burner lets you store more than 600MB of data in a format that can be exchanged with most computers. On top of that, you can create CD music disks!

Both graphical and command-line tools exist for creating CDs in Red Hat Linux. The `cdrecord` command lets you create audio and data CDs from the command line. The `xcdroast` provides a graphical interface. Both tools let you write to CD-Recordable (CD-R) and CD-Rewritable (CD-RW) drives. The cdrecord command and xcdroast window are described in the next section of this chapter.

Only SCSI CD-ROM drives can be used to create CDs in Linux with the current tools. If you have an IDE writable CD-ROM, however, don’t despair. With a bit of extra configuration, you can set up your drive for SCSI emulation. After that, Linux CD writing tools write to it as though it were a SCSI drive.

### Configuring an IDE CD-ROM for recording

If you are using a SCSI drive, you are probably ready to begin recording; CD recording tools in Linux should recognize and be able to use your drive automatically. If you are using an IDE-based drive, however, you may have some work to do.

In most cases, your IDE writable CD drive should be recognized and properly configured when you install Red Hat Linux. The following boot option should automatically appear as an option to your bootloader:

```
hdc=ide-scsi
```

This shows that IDE disk device "c"(hdc) is set up to do SCSI emulation. If this is working properly, you should be able to type the following to see if the CD drive appears on the list of accessible SCSI devices.

```
$ cdrecord --scanbus
```

If your IDE writable CD drive is not working, check that the following basic steps are done: 1) have SCSI emulation built into the kernel; 2) remove the IDE-CD module; and 3) add the IDE-SCSI module. By default, SCSI emulation should be built into your kernel, so unless you remove it, there’s nothing you have to do there. Here’s how you accomplish the other two steps:

1. To remove the ide-cd module, as root user add the following line to the /etc/modules.conf file (using any text editor).
