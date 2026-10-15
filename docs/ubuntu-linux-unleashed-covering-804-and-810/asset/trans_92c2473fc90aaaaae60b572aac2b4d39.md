

首次打开 F-Spot 时，系统会提示你导入第一批照片，如图 7.15 所示。你也可以为它们分配一个标签，以便跟踪特定类型的照片。你可能希望允许 F-Spot 将照片复制到新的目录 Photos——这有助于你在系统上整理照片。

![](img/8f9e74e2b343ff525bebfb720a3d8441_199_0.png)

FIGURE 7.15 The versatile F-Spot makes adding photos to your library easy.

准备就绪后，点击 Import 让 F-Spot 将照片导入库。图片会出现在 F-Spot 库中，并按拍摄日期存储。该信息由相机每次拍照时存储的 EXIF 信息提供给 F-Spot。在图 7.16 中，你可以看到标准的 F-Spot 窗口。

使用窗口顶部的 timeline 在照片中浏览，并可以通过双击任意照片进行一些简单的编辑。F-Spot 仍处于起步阶段，但开发正在进行中，因此请留意任何重大更新。

## Burning CDs and DVDs in Ubuntu

Linux is distributed across the Internet through the use of ISOs that are waiting to be written to CDs or DVDs. Therefore learning how to burn discs is essential if you have to download and install a Linux distribution. Not only that, but you are likely to want to use CDs and, more commonly, DVDs to back up your music, family pictures, or other important files. With DVD writers being so cheap, the format is now pervasive and more and more people use cheap DVDs as way of archiving simply due to the larger storage size available. Of course, you can use blank CD media, but they don't have anywhere near the capacity offered by DVDs albeit being slightly cheaper. Today's high-resolution digital cameras can occupy upward of 3MB per shot, and music files can be anything from 1MB to 10MB+ in size. These file sizes make DVD the obvious choice, but there are still occasions when you need to write to a CD. You can use CDs and DVDs to

![](img/8f9e74e2b343ff525bebfb720a3d8441_200_0.png)

**FIGURE 7.16** Browse through your extensive photo collection and correct minor problems using F-Spot.

- Record and store multimedia data, such as backup files, graphics images, and music.
- Rip audio tracks from music CDs (*ripping* refers to extracting music tracks from a music CD) and compile your own music CDs for your personal use.

Linux audio clients and programs support the creation and use of many different types of audio formats. Later sections of this chapter discuss sound formats, sound cards, music players, and much more. Because CD burning is used for many other purposes in Ubuntu, we cover the essentials of that process first in this chapter. To record multimedia data on a CD, you must have installed a drive with CD writing capabilities on your system. To make certain that your CD writer is working, use wodim -scanbus to get the information for using the CD drive under SCSI (small computer system interface) emulation:

```
# wodim -scanbus
scsibus0:
    0,0,0    0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
    0,1,0    1) *
    0,2,0    2) *
    0,3,0    3) *
    0,4,0    4) *
    0,5,0    5) *
    0,6,0    6) *
    0,7,0    7) *
```

这里，你可以看到 CD 刻录机（在本例中为 CD 刻录机/DVD 读盘机）已存在并且系统将其识别为设备 0,0。 这些数字代表设备的 scsi 总线/目标/lun（逻辑单元号）。刻录 CD 时需要知道此设备号，因此请记下或记住它。

## Creating CDs and DVDs with Ubuntu's Graphical Clients

Although adequate for quick burns and use in shell scripting, the command-line technique for burning CDs and DVDs is an awkward choice for many people until they become proficient at it and learn all the arcane commands. Fortunately, Ubuntu provides several graphical clients.

### Nautilus

With Ubuntu, enhanced functionality has been included in the default file browser Nautilus. Under the Places menu item is a CD/DVD Creator selection. To use it, insert a blank CD or DVD into your CD-R/DVD-R drive. You must have two Nautilus windows open: one that shows the files you want to save to the CD, and a second one open to the CD/DVD Creator Folder (accessed in Nautilus by the Places menu, CD/DVD Creator) location. Click on the Write to Disc button as shown in Figure 7.17 to bring up the Write dialog; at the next dialog box, choose the format to which you want to write the disc. Nautilus CD/DVD Creator supports writing to a disc image file, commonly known as ISO. You can also give your new disc a label and tell Nautilus at what speed you want to write the disc. Finally, click the Write button to start the burning process—it is that simple!

![](img/8f9e74e2b343ff525bebfb720a3d8441_201_0.png)

FIGURE 7.17 Creating a CD or DVD using the Nautilus browser is made easy with the drag-and-drop features it provides.

### Brasero

A relatively new addition to the Ubuntu default distribution is Brasero, an easy-to-use graphical CD and DVD burning application. Installed as part of the standard Live CD installation, Brasero is found under Applications, Sound and Video as Brasero Disc Burning.

