
# 28 Part I: Introducing Linux

![](img/96a9ce6a13d8d15ed05f867f41574278_55_0.png)

Figure 2-8: The mail compose window of exmh(1).

## Commercial mail interfaces

As with the text editors, several commercial mail interface programs are available. Some are sold as sole programs; others are part of application suites. One such product is Zmail, from NetManage Software. Zmail has been ported to many UNIX systems and also to Windows 3.1, 95, 98, and NT. Because Zmail works across many systems, you can use the same mail interface on all your platforms.

Another commercial mail interface is found in Applizware, produced by Applix, Inc. This product is an office suite consisting of a WYSIWYG (what-you-see-what-you-get) text processor, an integrated spreadsheet presentation package, a graphical editor, and a mail front end. In Figure 2-9, you can see the word processing package over to the left, the presentation package in the upper center, and the spreadsheet package in the lower center.

In addition to Applizware Office suite, another office suite is popular among Linux users: StarOffice. StarOffice is a full-featured office suite that was gained by so much popularity among Linux users that it was bought by SUN Microsystems.

## Chapter 2: Accessorizing Linux

![](img/96a9ce6a13d8d15ed05f867f41574278_56_0.png)

Figure 2-9: Some of the applications in Appluxware Office Suite.

## Multimedia Programs

Linux typically comes with a series of programs for simple drawing and painting as well as image viewing, conversion, and manipulation. It can display still and animated images and can record, manipulate, and play back audio (given that your hardware has a supported sound card). This section gives you a sampling of some multimedia freeware programs that you can use with Linux.

xpaint is a simple drawing and paint program that you can use to read in an image and then perform simple manipulations of the image. xfig is a some-what more sophisticated drawing tool. xpaint is not included on the CD-ROM.

ImageMagick is a freely distributed program for graphical image manipulation. This program can read many types of images, make them larger or smaller, cut portions of them, transform several images into an animation, and store the images back to disk in a different format (if desired). ImageMagick is included on the CD-ROM.

gimp is a graphical image-manipulation program based on plug-ins, which extend a program's capabilities. a gimp feature we like is the intelligent scissors feature, which enables you to cut out parts of a photo and paste them onto another photo (as in the movie Forrest Gump). gimp is included on the CD-ROM.

Ghostview is a program for viewing files from PostScript, an industry-standard page language for high-end printers. Ghostview uses a program called Ghostscript (Aladdin Enterprises) to print PostScript files to a dumb printer (one does not have a PostScript program built into it) or to put PostScript files out to a FAX machine. Newer versions of Ghostscript have distribution limitations, but older versions are freely distributable. Ghostview is included on the CD-ROM.

maxim(1) is a program for playing back stills, animations, and video — including any audio — in various formats. The program can also attach audio streams of various formats to the video if it does not already have an audio track. maxim is included on the CD-ROM.

A series of programs mix audio, play back audio, and even mail audio programs. For instance, cdplay(1) is a character-cell rendition of a program to play audio CDs (assuming that your system has a sound card). xplaycd(1), shown in Figure 2-10, is a graphical interface for playing a CD. Unfortunately, neither cdplay nor xplaycd is included on the CD-ROM.

The mixer program controls the volume of your sound. You can also mute the sound from the control panel, for those times when your or your teenage children come into the room complaining about the music you're playing. mixer is not included on the CD-ROM.

Figure 2-10: An example of the xplaycd program.

![](img/96a9ce6a13d8d15ed05f867f41574278_57_0.png)

## Part II
# Installing SuSE Linux

## The 5th Wave
By Rich Tennant

![](img/96a9ce6a13d8d15ed05f867f41574278_58_0.png)

> "THAT REMINDS ME—I INSTALLED WINDOWS 95 ON MY 386 LAST WEEK."

## In this part ...

You're about to embark on a journey through the SuSE Linux installation program. (If your SuSE system is already installed, you can skip this part and peruse another one.) Perhaps you know nothing about setting up your operating system on your computer. That's okay. SuSE Linux is smart and reasonable. Plus, you have to guide you.

In Chapter 3, you find out what SuSE Linux needs as well as what your system has in terms of hardware. Then, after backing up your system, you can move on to the next chapter, where you do more all-important preparation, such as creating a boot floppy disk. You also find out how to squeeze the data on your hard disk so that you can fit SuSE Linux there.

Next, you get to do what you've been waiting for ever since you bought this book: install SuSE Linux. Like park rangers, we guide you along the various trails of the installation process, pointing out pitfalls and cautioning you about hazards. You get to enjoy the views, too, as you move screen-by-screen through your trek.

Your travels through the installation may not be over yet, however. Installing X Window System can be tricky, which is why we provide an entire troubleshooting chapter on it. So, if you decide to include X Window System and have problems installing it, Chapter 6 is for you. If you installed X Window System without a hitch, break out the trail mix and enjoy a well-deserved rest.

Finally, in Chapter 7, you reap the benefits of all your efforts and use SuSE Linux for the very first time. Happy trails.

## Chapter 3
# Discovering What's in Your System

### In This Chapter

- Figuring out the resources
- Unearthing the type of hardware

The function of this chapter is to help you install Linux. If your system is already installed, count lucky and find out what lies inside. We would like to dispel a myth that Linux is harder than Windows. We believe that Linux is no harder than any other operating system. The easiest way to install Linux is to buy it preinstalled. If you have an SMP system, would you like to trade with me?

The Intel processor should have the following amount of RAM:

- Without graphics, Linux runs (er, walks) with 8MB.
- With graphics, we strongly advise you to have at least 32MB of RAM.
- With 64MB, Linux works quite well and the speed of the application (particularly a graphics-oriented program) increases dramatically.
- 128MB can be found in the systems of some Linux developers because they tend to run many programs at a time, and each program takes up a certain amount of RAM when running.

#### Installing SuSE Linux

If you're like most readers, however,

- Want to install Linux to your existing hardware own- Want to use existing disks
- Want to keep MS-DOS, or Windows, or both on your system

You've chosen the hardest of installation. Don't worry, though, because we're here to guide you through it.

### Hardware Supported by Linux

Generally, Linux has been ported to run on many platforms, such as any Intel processor that is a 386 or newer, as well as on Digital Alpha, Sun SPARC, Motorola, MIPS, PowerPC, and HP/PA platforms. SuSE Linux has been ported to the Intel and Alpha platforms and is considering additional platforms in the future. The SuSE Linux Dummies CD-ROM works only on Intel PCs, and what is discussed in this book. If you want to install SuSE Linux onto an Alpha, don't despair: The platforms aren't that different and you can probably adapt the instructions. You'll need to buy a different CD-ROM than the one in the back of the book, however, because it supports only the Intel line of processors.

Linux supports symmetric multiprocessing (SMP), which means that you can have more than one CPU per box. In fact, it supports several processors per system box. If your system has more than one CPU, Linux will be able to utilize those CPUs also, either by speeding up a specific program written to take advantage of multiple CPUs or by allowing more programs to execute at one time. If you have an SMP system, would you like to trade with me?
