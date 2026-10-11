
![](img/0e9cf4c65a042f4a9bea644dc50153a7_129_0.png)

![](img/0e9cf4c65a042f4a9bea644dc50153a7_129_1.png)

**Tip**

People with a three-button mouse can click the applet using the middle button and drag it to wherever they want. Scroll-wheel mice offer similar functionality because most wheels are actually a third button (try clicking your mouse wheel). It’s not unusual for applications in the Linux world to take advantage of the middle mouse button, but its use is often overlooked.

Have another look at that menu and you’ll see that there are some other useful options. For instance, each application may have its own set of configurations. The fish applet I had you install comes with a small handful of additional graphics—you may not like fish. Just click the Preferences menu to make your changes. Finally, should you decide that the program you chose is just taking up space, there’s a Remove option.

When the applet mania has taken hold, you may find yourself out of space. Yes, it is time to add another panel. Right-click somewhere in your panel’s empty space. From the pop-up menu, select New Panel. A blank, gray panel appears; you can drag it to any location that you see fit. As with the original panel, selecting the properties dialog allows you to change the size to fit the applets you have in mind.

I’m going to share some of my favorites with you, although they are not all entirely useful in terms of work. The Dictionary Lookup applet is a must, as is the Weather Report program. The fortune Fish (mentioned earlier) is fun, as are the eyes that follow your mouse pointer around the screen. The Take Screenshot applet is particularly useful when you are doing documentation. Because I work on a variety of systems, I’m also rather fond of the Terminal Server Client and the Connect to Server applets. (I briefly mentioned this last one in Chapter 4, but via Nautilus.)

I’m going to leave the discussion of applets here, but I invite you to try others and discover your own favorites. Go ahead. Explore!

## Miscellaneous Changes

Let me give you one final *treat* before I close this chapter: Click **System** on the top panel, and then select **Keyboard Shortcuts** from the **Preferences** menu. You’ll discover lots of interesting keyboard shortcuts to do things such as switching from one application to the other, switching from one workspace to the other, opening and closing windows, getting help, taking a desktop screenshot (in case you want to share your fashion sense with others), and so on.

## Resources

**GNOME-Look.org**

http://www.gnome-look.org

**Art.GNOME.org**

http://art.gnome.org

This page intentionally left blank

# Chapter 6

## Printers and Other Hardware

> Ah, hardware . . . "I hate hardware!"

Part of the personal computer experience seems destined to be an eternal battle in getting your current system to talk to the latest and greatest devices. There's always a new, hyper-fantastic, 3D video card, mind-blowing stereo sound system, or hair-trigger game controller out there. Then there are everyday devices, such as modems, scanners, and printers. Getting all these devices to work with your system is something that has caused us all grief over time, regardless of what operating system we were running.

We are used to assuming that anything works with Windows, but even that isn't true. From time to time, even Windows users must visit hardware vendors' Web sites to download a driver. One of the things that sets Ubuntu Linux apart is its intelligent and accurate hardware detection and support. Most things will be automatically configured without a fuss. In this chapter, I'm going to give you the tools you need to deal with common issues and give you some tips on avoiding problems in the first place.

## Yes, It Runs with Linux!

Device support under Linux is excellent. The sheer number of things that will work “out of the box” without you having to search for it install drivers is impressive and, quite frankly, beats your old OS. That doesn’t mean all is rosy, however. Let me be brutally honest here. Some devices have been written to work with Windows and only Windows . . . or so it seems. One of the great things about this open source world is that developers are constantly working to write drivers to make it possible to run that faster-than-light communications card.

If you haven’t already bought that new gadget, there are a couple of things that you should do. For starters, if you are in the store looking at that new printer, pull the salesperson aside and ask whether it runs with Linux. If the person doesn’t know (which is sometimes a problem, but less so as time goes on), take a few minutes to check out the excellent Hardware HOWTO document. You can always find the latest version by surfing on over to the LDP’s Linux Hardware Compatibility HOWTO page:

http://www.tldp.org/HOWTO/Hardware-HOWTO/index.html

If you don’t find what you are looking for there, check out the hardware compatibility guide on your Linux vendor’s site. In the case of Ubuntu Linux, that means paying a visit to the Ubuntu Wiki and checking out the hardware support pages:

https://wiki.ubuntu.com/HardwareSupport

> *Quick Tip* Red Hat’s hardware catalog is also worth the visit, regardless of what version of Linux you are running. The URL follows. However, keep in mind that URLs do change on Web sites. If you don’t find it there, just go to the main Red Hat site at `http://www.redhat.com` and look for *hardware*.
> `http://bugzilla.redhat.com/hwcert`

Although Ubuntu Linux is Linux, different releases of different vendors’ products may be at different levels of development. Consequently, at one time or another, Red Hat may have slightly more extensive support for hardware than the others, and a month later SUSE may have the widest range of support.

As Linux gains in popularity, you'll find that hardware vendors are increasingly interested in tapping into this ever-growing market. I've had the experience of being on site, adding hardware to a customer's system (Ethernet cards come immediately to mind), and finding that the system did not have the drivers. I quickly visited the Ethernet card manufacturer's Web site and found precompiled drivers ready and waiting for me.

## Plug and Play

For the most part, adding a device to your Ubuntu Linux system is simply a matter of plugging it in. If the device doesn't just appear and you don't want to configure it manually, a reboot forces hardware detection, and the device should be recognized by the system and configured. Universal Serial Bus (USB) devices tend to be even easier because of their hot-plug nature. In other words, you don't need to reboot the system in order to have a USB device recognized, and you can unplug it while the system is running. For instance, plug in a USB key or USB pen drive and it simply appears in your Places menu (see Figure 6-1).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_135_0.png)

**Figure 6-1** A 128MB USB drive appears in the Places menu (note that the formatted size of the drive is only 120.1MB).

Getting a device recognized is only part of it, though. Just because your system knows about the device doesn't necessarily mean that it is configured for your applications. Although you generally don't have to find and install drivers, it does happen, just as it does in the Windows world. It wouldn't be fair to you if I simply ignored this little tidbit, so I won't.

Let’s take a look at the most popular, and sometimes the most frustrating, piece of hardware computer users are faced with. That’s right, I’m talking about printers.

## Printers and Printing

This might seem like a silly thing to mention, particularly if your printer was automatically detected, configured, and tested at boot time. Nevertheless, there are things that you might want to do with your printer, and we should probably cover some of these now. Furthermore, printing is one of the most important functions a personal computer can perform. It’s good to get it right. On that note, I’m going to spend a little bit of time talking about printers and printing. *Trust me, it’s going to be lots of fun.*

Printing under Linux works on the basis of *print queues*. At its simplest, this means that whenever you send something to the printer, it is queued in a directory where it awaits its turn at the printer. This de-queuing is known as *spooling*. Consequently, the process that sends the print jobs from the queue to the printer is called the *spooler*. That spooler can be one of a small handful of programs, all of which are transparent to you when you print from applications. Here’s a quick roundup of the more popular spoolers.

CUPS, the Common UNIX Printing System, is designed to be a platform-independent printing system that works across a great number of UNIX flavors, including Linux. CUPS uses the Internet Printing Protocol (IPP), a next-generation printing system designed to allow the printing of any job to any printer, anywhere. At this point, CUPS certainly looks like the spooler of the future. Most modern Linux distributions include CUPS, and Ubuntu uses it transparently.

The second most likely spooler you run into is LPD, the classic UNIX spooler. LPD has been around for a long, long time and continues to be distributed with pretty much every Linux out there. I mention it mostly for historical reasons. It’s there, but you won’t likely be using it.

Whether it is CUPS or LPD, GNOME handles printing beautifully. Adding, configuring, or removing a printer is done through the system printing
