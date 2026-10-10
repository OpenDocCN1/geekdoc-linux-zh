
## Distros

For installing DEB files – ideal for those who are command-line averse.

From the Activities view, find the Pop! Shop launcher either by typing it or selecting the Show Applications button on the dock to the right, pausing for a second to admire the bold icon design. You could say that Pop! OS's initial app offering is quite sparse, but the idea is that you add only what you need to it. Not everyone wants Visual Studio Code or Slack, but if you do they're very easy to find in the Pop! Shop.

Today’s application picks are brought to you by the letter G: Goxel – making voxel art is surprisingly calming; GNOME Twitch – for watching Gaming on Linux videos; and GIMP, which is still the best way to manipulate images.

Naturally, command-line installation with apt is possible too, and many packages don't have a Pop! Shop entry. One thing missing from the Pop install is the OpenVPN plug-in for NetworkManager, which if you use a VPN (or envisage doing so in the future) you'll want to remedy with:

```
$ sudo apt install network-manager-openvpn-gnome
```

We hope your Pop install doesn't break, but if it does help is at hand in the form of a recovery partition. This essentially lets you boot to something like the Live environment on the DVD, from whence repairs can be carried out. Press Shift and Escape while the system is booting and select the recovery environment from the menu. If that doesn't work you can perform a Refresh Install, which resets all system configuration and applications, but retains your user information and documents, much like the equivalent Windows utility.

Speaking of booting the system, Pop is pretty much unique among major distros in that it uses System-boot – formerly Grubmbout – to boot the system on UEFI installs. This means that for once we can say you won't run into any horrible GRUB problems on this distro, unless you use classic-BIOS booting. You shouldn't run into any System-boot troubles either, by the way, as System76 test all kinds of weird and wonderful configurations on its hardware.

The included video player is fine, but you may prefer to install MPV, which handles its own codecs. Once installed it also takes advantage of whatever hardware acceleration is on offer (VDPau, VA-API or some unholy combination of the two is configured out of the box) to decode video without bothering your CPU.

The Pop! OS team has done a great job of preparing documentation too. There's a growing list of guides to common tasks at https://support.system76.com/articles. For example, if all the abstract references to terminal commands throughout this magazine make no sense to you, find out more in the Terminal Basics article there.

The team are enthusiastic about getting more people involved with development, too. They even mark out specific bugs in their project as being 'bite-size', suitable for aspiring coders to cut their teeth upon. We have to credit them for this, as the growing divide between users and developers will only be lessened if more people get involved, and such outreach efforts are a fine way to encourage that kind of involvement.

We also must credit System76 for its excellent open hardware efforts. Besides contributing to open firmware causes, its flagship Thelio machine includes a custom daughterboard for managing airflow. The specs for this are completely open, and System76 hopes to develop more hardware that follows this mode. We're definitely excited to see more.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_47_0.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_47_1.png)

### Choose Your Own Adventure

“Pop! OS’s initial app offering is quite sparse, but the idea is that you add only what you need to it.”

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_48_0.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_48_1.png)

**Installing Pop! Alongside Windows**

1.  **Write an install medium**
    If you have an Nvidia graphics card you'll want to fetch the Nvidia build from https://system76.com/pop and burn it to a DVD or write it to a USB stick. If you have trouble booting Pop_OS from the LXF DVD (or have no DVD drive), you should write the ISO file from the Pop/ directory (or the link above) to a USB.

2.  **Make space**
    Start Windows and open the Disk Management tool. The easiest way to find it is by opening the start menu and typing the first few letters of 'disk man'. Right-click the C: drive and choose Shrink Volume. Make some space for Pop. Pop recommends at least 20GB, but if you can spare it, use it.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_48_2.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_48_3.png)

3.  **Boot Pop!**
    Boot Pop_OS and start the installer. After answering some localisation questions choose the Custom (Advanced) option, unless you're happy to get rid of everything on the target drive. Select 'Modify partitions', right-click the Unallocated Space and click New. Go with the defaults and then click Add and finally Apply the changes.

4.  **Select partitions**
    Exit the partitioning tool and click the new partition. Click the 'Use partition' switch, again leaving the defaults. Click the EFI partition (it's usually second from the left on a Windows install and is FAT32-formatted) and again use it as a Boot partition, but please don't format it as that will break Windows.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_48_4.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_48_5.png)

5.  **Lift off**
    Hit Erase and Install to begin the fun. Either watch the progress bar intently or make a cup of tea. When the installer's done hit Reboot and do some final setup steps. You can enable location services and connect online services. Finally, set up a user and password, then click the big tick to start using Pop!_OS.

6.  **Update and augment**
    The 'Updates' will probably be available. You should install these when prompted, then switch from the Installed tab to the Home tab. Here you can peruse the multitude of applications awaiting your attention in the Pop!_Shop. Pop is deliberately lean out of the box, so you may want to install some workhorse applications at this point.

## Do more

- 052 Lock down Linux
- 060 Ransomware
- 068 Virtualise
- 078 Cloud
- 082 Malware
- 090 Benchmark
- 094 Audio
- 098 Music
- 104 Embedded

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_49_0.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_49_1.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_50_0.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_50_1.png)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_50_2.png)

## Lock Down Linux

It may be the end times out there but **Jonni Bidwell** will ensure your Linux boxes are equipped to weather the storm.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_51_0.png)

**W**hen you install Linux on your desktop, then as long as you install an up-to-date distro the chances are you're reasonably secure. The same is true for servers, as long as you choose a strong password (or disable password access altogether and use SSH keys instead). There's a faction of the Linux-using populace that still likes to bang the “Linux is more secure than Windows” drum, but this isn't really true anymore. Both Linux and Windows have multiple layers of security coded by very smart people. Both Linux and Windows rapidly patch emergent security issues. And neither Linux nor Windows can do a whole lot about flaws in whatever software people choose to run on them, and they certainly can't do anything about users configuring that software in an overly permissive manner.

> **WHAT'S TO COME…**
> “We will look at everything from next-gen logins with hardware tokens to basics like SSH keys.”

We'll look at how to shore up defences on Linux, whether on the desktop, server or up in the clouds. We'll cover passwords, keys, firewalls and much more to keep your data safe. We'll focus more on security than privacy, so won't be talking Tor, VPNs or Whonix, but there's no reason why these can't be used with the setups we'll discuss.

What we will look at is everything from next-gen logins with hardware tokens to basics like SSH keys. We've also got tips for shoring up Nextcloud and more. Let's start with a survey of Linux security features, and how they get thwarted.
