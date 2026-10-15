
Dual booting does have certain advantages. Although your computer's performance running Linux alone is never impeded unless you run VMware, the guest operating system in VMware always runs somewhat slower than it would if it had complete control over the computer's resources.

Also because guest operating systems do not have complete access to your PC's hardware, there might be certain devices you cannot use properly, or at all, in a VMware session that would work if you booted directly into the OS. (Hardware compatibility is further discussed in Chapter 2, "Understanding How VMware Works.") Table 1.1 provides a quick comparison of the features and drawbacks of VMware and dual-boot environments.

Table 1.1 Comparison between VMware and Dual Booting

| Method | Advantages | Disadvantages |
|---|---|---|
| VMware | Simultaneously run multiple OSs<br>Easy to install/configure | Extra expense<br>Guest OS partially slowed |
| Dual boot | No added cost<br>Full, native hardware support | Difficult to configure<br>Switching is inconvenient |

> For more information on dual booting, and a variety of other topics, head to the Linux Documentation Project at http://www.linuxdoc.org.

## VMware Versus DOS and Windows Emulators

VMware was by no means the first product to try to bring Windows compatibility to Linux, although it is unique in its virtual machine approach.

## Emulation, like Fine Wine...

One of the oldest, and probably the most famous Windows emulator, is Wine. Actually, "emulator" isn't quite the right term for Wine (which is an acronym with multiple meanings, one of which is "Wine Is Not an Emulator").

## Bochs: Full PC Emulation

Bochs was designed to be highly portable and has been compiled and run successfully on a variety of different computer architectures and operating systems. That's because Bochs is a true emulator, rather than a virtual machine.

Remember the difference? Bochs is based around an Intel 386/486/Pentium CPU emulation, which runs even if Bochs is used on a Pentium-based Linux PC. This makes Bochs a consistent product across all the supported platforms, but also means it is slower than a true virtual machine such as VMware. It also has ridiculously cluttered configuration files that make DOSEMU look easy to manage. See Figure 1.6 for a sample Bochs session.

Bochs was recently purchased and released as open source by MandrakeSoft, publishers of the Linux-Mandrake distribution. The original author of Bochs, Kevin Lawton, is now hard at work on Plex86, an open-source virtual machine project.

> To learn more about Bochs, head for http://www.bochs.com.

VMware's easy-to-use configuration interface alone is sufficient reason to give it the nod above these alternatives. VMware is also the only way to obtain full compatibility with Windows 95/98, Windows NT, and Windows 2000. Although each has its place—and might even find a place in your emulation strategy over time—VMware provides the fastest and most flexible way to run MS-DOS and Microsoft Windows applications under Linux.

It's also important to keep in mind that VMware does more than simply provide an emulation bed for Windows applications. With VMware, you can run another complete session of Linux or FreeBSD, and VMware's programmers continue to work to expand the range of operating systems that run inside the virtual machine. Although Bochs's support for other operating systems is slowly growing, VMware provides the widest range of guaranteed compatibility.

![](img/b2b6702758c230ce537468351fc8af15_36_0.png)

Figure 1.6 The Bochs PC emulator, loading the WebSpyder Web browser.

## Conclusion

You should now have a basic understanding of the technology behind emulators and virtual machines, and you have seen a glimpse of the potential of VMware to let your Linux PC expand its reach and software compatibility.

Chapter 2 describes the inner workings of VMware in greater detail and explains the extent of VMware's compatibility with various PC hardware and software configurations.
