
## Installing Miscellaneous Devices

As with any other virtual machine, if you have sound configured on the Linux host, you can make a virtual SoundBlaster 16 (minus MIDI capability) available to DOS programs.

To ensure that DOS applications properly find the sound device, you should edit autoexec.bat and add the following line, as shown in Figure 14.12:

```
set blaster=A220 I5 D1
```

This should enable old DOS programs to properly see the sound hardware and help newer "autoconfig" programs find the interface more quickly.

> The full specification of the virtual sound card: It is located on IRQ 5, DMA channel 1, 16-bit DMA channel 7.

Most DOS applications do not contain their own mouse support: They expect to see a mouse driver residing somewhere in DOS memory.

Newer editions of DOS typically come with a mouse driver (usually known as MOUSE.COM or MOUSE.EXE). You have nothing to lose: Try typing MOUSE at a DOS prompt and see whether the driver starts. If not, a quick Web search on the technical support download areas of mouse manufacturers, such as Logitech, should yield quick results. Any reasonably modern mouse driver should detect the generic virtual mouse.

You can run the mouse driver whenever you need mouse access or add a call to the MOUSE program to the autoexec.bat file if you prefer.

![](img/b2b6702758c230ce537468351fc8af15_301_0.png)

![](img/b2b6702758c230ce537468351fc8af15_301_1.png)

## Applications and limitations in DOS

Between Windows and Linux, you may have forgotten, but for over a decade DOS was the single most popular business and home operating system. Surely, you can think of something you're interested in running.

### Installing Useful Programs

Your first order of business, after you've completed all the installation steps, should be to get your hands on a DOS-compatible UNZIP tool. You can download a self-extracting MS-DOS version of PKZIP from http://www.pkware.com.

The DOS PKZIP archive is only a few hundred kilobytes in length. Shuttle it to the virtual machine using a floppy disk or virtual drive mounting, and run the self-extraction program. Then copy PKUNZIP.EXE to C:\DOS or another directory in the DOS command path.

After that, you're ready to install most any freeware/shareware package out there, and there are certainly plenty that have been created in the 20 years since DOS was introduced. Most commercial applications that can operate within the limitations of the DOS virtual machine (see next section) will be perfectly happy to run in your VMware window. See Figure 14.13 for an example.

Although enthusiasm for developing and maintaining new productivity applications for DOS has certainly waned in recent years, familiarity and speed of execution are important to many people. This may be your big chance to get back into classic Lotus 1-2-3!

![](img/b2b6702758c230ce537468351fc8af15_302_0.png)

Figure 14.13 The venerable WordPerfect for DOS, as well as tens of thousands of other programs and games, await you.

On the other hand, given the state of applications for Linux, to say nothing of the availability of Windows through VMware, it could be that you want to use DOS primarily for gaming. Gaming with VMware is covered in Chapter 15, "Playing Games with VMware."

### Working Around VMware-Related Limitations

I've already mentioned that VMware does not support expanded memory (EMS) in DOS, which is a shame because some programs insist on having access to EMS. There's really nothing to be done until and unless VMware decides that the problem is serious enough, and of enough concern to their customers, to fix. You can have all the extended memory (XMS) you like, which is some consolation.

A quick browse through this chapter should betray another major problem with VMware and DOS: There is no VMware Tools step. No accelerated, high-color graphics driver and no custom mouse interface or disk shrinking tool.

When you use a DOS virtual machine, you are limited to plain VGA capabilities: a graphics screen of 640×480 resolution and 16 colors or 320×200 resolution and 256 colors. That's adequate for a wide range of DOS applications and even games, because plain VGA wasn't a common standard until the early 90s and developers couldn't always assume their customers had video cards capable of supporting SVGA and beyond.

There is another interesting problem running DOS in VMware. Remember the VMware CPU sharing model? It only works the way it is intended to when the guest operating system shows a little cooperation and doesn't try to hog the CPU when applications are not running. Unfortunately, most versions of DOS do not properly "idle" the CPU even when they are not busy, which can cause VMware to occupy an abnormally large share of CPU time when you are working in the host instead of the guest.

A small program called DOSIdle solves this problem by correctly "throttling" the CPU to low levels of consumption when DOS is not in use. This frees up resources for the Linux host.

To use DOSIdle, follow these steps:

- 1. Download the DOSIdle archive from http://www.vmware.com/software/dosidle210.zip. (You might want to rename it to something that complies with the DOS 8.3 filename limits, such as simply dosidle.zip.)
- 2. Using the method of your choice, copy the dosidle archive to a new directory on the virtual disk, c:\dosidle.
- 3. Unzip the archive, probably by typing pkunzip dosidle.zip.
- 4. Type dosidle at the prompt. You should see a short printout summarizing your virtual machine's configuration, shown in Figure 14.14.
