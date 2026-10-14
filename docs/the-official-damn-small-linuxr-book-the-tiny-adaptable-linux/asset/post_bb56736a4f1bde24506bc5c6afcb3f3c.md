
Making a digital media frame can be a fun project. But before diving into it, I strongly recommend you read the following warnings regarding both the hardware and software aspects of this project:

- **Hardware Warning!**—In making a digital media frame, you need to take apart a laptop computer in such a way that it will probably not go back together again. So, if you want the laptop to be a laptop again, don’t use it for this project. Also, it is quite possible that you might do irreparable damage to the laptop in the process of adapting it into a digital media frame. So, please don’t use a laptop that you can’t afford to be without. Finally, the resulting media frame will not be UL approved (www.ul.com), so you run some risk of burning your house down.
- **Software Warning!**—This is not a click-and-go project on the software side either. In this project, you repartition disks, modify bootloaders, and work with initialization scripts. If you find the command line to be challenging, you will probably find this project difficult to do.

The bottom line is that this project is for more advanced Linux do-it-yourselfers who have an old laptop to spare. If that’s not you, you might want to limit yourself to playing with some of the multimedia software described in this chapter.

## SETTING PROJECT GOALS

In its most basic form, a digital picture frame simply plays a bunch of digital images it is given, without needing any intervention, after it is booted up. The images are usually played as a slideshow, with the images changing automatically every few seconds.

To make this project different from basic digital picture frames, I want to expand the features in the following basic ways to make it more as a digital media frame:

- **Play different media types**—Allow the unit to play music, presentations, or videos, along with digital image slideshows. So, for example, the frame could be set up to loop a video at a trade show or a real estate open house.
- **Make it easy to add content**—Set up ways to add any of the supported content types easily, using different types of network connections (wired or wireless), as well as removable media (such as a USB pen drive).

Shopping for the software for the project is easy (it’s all on the CD that comes with this book). For me, getting the frame meant sending my wife Sheree on a trip to find a picture frame that is more than two-inches deep and large enough to display the laptop's screen. After that, a few extra pieces for mounting the laptop in that frame are needed. But the big chore is finding the right laptop at the right price.

## CHOOSING A LAPTOP

When you go to search for a laptop to use for your media frame, you need to decide if time or money is more important. The cheaper the laptop, the more probable that it will require extra work to do the things you want it to do. Also, be aware that replacement parts can sometimes cost more than the value of the laptop itself (especially if you need to add RAM or replace a broken screen). So, in general, the cheapest laptop may not be the best choice.

### Asking About a Used Laptop

Old laptops are available everywhere from garage sales to online sites. If you are heading to a used computer store or online auction to get a used laptop, here are some things you should check for:

- Working?—Many older laptops are being sold for parts only. If you are purchasing a laptop online, be sure to get a guarantee that if it is not working, you can return it. If you have access to the laptop before you buy, take your handy Damn Small Linux CD and a boot floppy with you to see if the laptop can boot DSL. (While the laptop is booted, use DSL to check out what's available—disk space, RAM, etc.—as described in the “Evaluating a Used Laptop” section in this chapter.) Keep in mind that our definition of working is not the same as other people's definition of working. For example, a missing hard drive and a few broken keyboard keys might get you a good price, but still work fine for your digital frame. Without a hard drive, you can run the project from CD and get images over your LAN or from a USB flash drive.
- Boot media—Some older laptops don't have CD drives. That poses problems not only for booting, but also for accessing the 50MB image you need to run Damn Small Linux. A 3.5-inch floppy disk was the standard removable boot medium before CD drives became popular, but it can only hold up to about 1.7MB of data at a time (although it is referred to as a 1.44MB floppy). Using floppy disk installation procedures and a stack of 35 floppies (see Chapter 8, “Installing DSL in Alternate Ways”), you can get DSL on to a hard disk and boot from there.
