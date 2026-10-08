
The installation script starts the VMware *daemons* (programs that run continuously in the background to provide system-wide services) and asks whether you want to share files with the virtual machine.

9. Press Enter.
10. Enter the username and password of an account on the host machine. For example, you should enter the username and password of your Linux account. When the script prompts you for your SMB password, use your Linux password.
11. You're prompted to enter additional usernames and passwords. Enter yes if you want to do so. Otherwise, press Enter to accept the default No answer, and the configuration process ends.

The VMware server is now configured on your host machine. The `vmware-config.pl` script starts up the virtual machine processes when it finishes. You can rerun `vmware-config.pl` whenever you want to reconfigure VMware.

## Installing an operating system on a virtual computer

VMware is great at providing a platform on which to run other operating systems under Linux. You can install either Windows or Linux on your virtual PC. After you install and configure VMware, you can run and use your virtual PC.

This section describes how to install Linux on your new VMware Workstation. We use Linux because we can't include Windows on the companion DVD or expect you to go out and purchase that expensive puppy. (We asked Microsoft whether we could bundle its operating system, but we never heard back about it. Not until recently did we realize that it uses a different license from Linux. Just kidding!) Because we can, and already do, bundle Red Hat Linux, we can easily show you how to install it. However, if you have a legal copy of Windows, go ahead and install it.

### Creating a VMware icon on the GNOME Panel

You start the installation process by first creating a GNOME applet that you click to start VMware. This action makes starting VMware a breeze. Follow these steps:

- 1. Right-click the Gnome Panel and choose Panel⇢ Add to Panel⇢ Launcher.
- 2. Enter, on the Name submenu, the name you want to call your icon; for example, VMware.
- 3. Enter any information you want in the **Comment** field and then type `/usr/bin/vmware` in the **Command** field.
- 4. Click the **Icon** button and a selection of numerous generic icons appears. Select any one that tickles your fancy.
- 5. Click the **OK** button. The new launcher appears on the GNOME Panel.

### Starting your virtual machine

Now, you use the new icon to start your VMware virtual machine. The following steps describe how to start the machine:

- 1. Click the **VMware** icon and the **VMware Workstation** appears.
- 2. You need to enter your evaluation license serial number, so choose **Help>Enter Serial Number**.
    - Enter the temporary serial number that was e-mailed to you. Also, enter your name and, optionally, your company name.
- 3. Click the **OK** button and then click **New Virtual Machine**.
    - The **New Virtual Machine Wizard** opens. The default setting should work for you, so you don't have to make any changes.
- 4. Click the **Next** button, open the **Guest Operating System** pull-down menu, and choose **Linux**.
    - You can safely accept the default settings in the next set of steps.
- 5. Select **Use Network Address Translation (NAT)** when you see the **Network settings** window and then click the **Finish** button.

Congratulations! You have started your first virtual computer.

### Installing Red Hat Linux on your virtual machine

You have your virtual machine running, so what can you do with it? You can install Linux and Windows and on it. The next step in the process installs Red Hat Linux on that virtual computer:

- 1. Insert the companion **Red Hat Linux DVD**.
    - Alternatively, insert a Windows CD in the drive, if you have one. Proceed through this set of steps and substitute the Windows installation process where appropriate.
- 2. Click the **Power On** button.
    - The VMware workstation starts up. You see the BIOS menu, just like you do on a real machine. The virtual computer should detect your Red Hat Linux CD and start the installation process, just like in Chapter 3.

![](img/8c094d1b36276212c03d10d898508a6e_214_0.png)

- 3. **Install Red Hat Linux.** The installation process is the same as we describe in Chapter 3.

VMware uses simple Linux files on the host machine to simulate the virtual computer's disk partitions. (You have the option to use a separate partition for the virtual computer, but the most common method is to use the host file.) Installing an operating system (OS) on a VMware virtual computer places the operating system's virtual disk on a file. Therefore, you don't have to worry about harming your host computer whenever you're installing a virtual OS. Any problems you encounter during the installation or use of the virtual OS are limited to the host computer files. The files used for the virtual OS are labeled with the .vmdk suffix.

- 4. **When you're prompted for the network configuration, select DHCP.**

Using DHCP shortens the network configuration process because you don't have to select a static IP address, netmask, and other parameters.

- 5. **When you finish installing the operating system, click Reset.**

Your virtual PC reboots and you have a fully functional virtual computer running Red Hat Linux. Cool.

Experiment with your newfound tool. Virtual machines provide you with a new killer application that can be used to do almost anything you want it to do. You have an exciting, fun, and powerful device.

![](img/8c094d1b36276212c03d10d898508a6e_214_1.png)

VMware creates not only virtual computers, but also virtual networks. Each virtual computer you configure to use bridged networking connects to a virtual switch. If you create two virtual machines on a single host, therefore, each machine can communicate with the other — and the host itself — as though they were connected to an Ethernet hub. This capability allows you to create experimental and production virtual networks. For example, you can use a single powerful PC to create several virtual servers rather than purchase and maintain individual ones. Cool.

![](img/8c094d1b36276212c03d10d898508a6e_214_2.png)

Plex86 is the open source world's answer to VMware. The Plex86 system provides a virtual computing platform similar to VMware in function. Plex86 works, but at the time this book was written was still in alpha development — it cannot run production systems. We encourage you to experiment with the system, which you can find at http://plex86.sourceforge.net.

# Part IV
Revenge of the Nerds

![](img/8c094d1b36276212c03d10d898508a6e_216_0.png)

> "Drive carefully, remember your lunch, and always make a backup of your directory tree before modifying your hard disk partition file."

## In this part . . .

In the great tradition of slackers and procrastinators, we have put off the real work as long as possible. In this part, you find out about how to make a server out of your Red Hat Linux computer. These chapters don't turn you into a Linux guru capable of commanding six-figure consulting fees, but they introduce you to the technical side of Linux.

We start by describing in Chapter 15 how to build a simple Local Area Network (LAN). Building a LAN isn't as difficult as it first sounds. You need to connect your computers, configure them to recognize each other, and then create an Internet gateway or firewall.

Chapter 16 shows how to use your Red Hat Linux computer as a network server on your newly created network; you can also provide services to the Internet.

We get serious in Chapter 17 and describe how to quickly but effectively secure your servers and network. This chapter is really an introduction to security methods and systems.

If (okay, when) you need to troubleshoot Red Hat Linux, check out Chapter 18. It provides some detailed help in fixing computer problems, with a special focus on networking. When you're done with this part, you'll be wearing pocket protectors with the best of us!

Chapter 19 returns from the serious world of computer security to have some fun. The chapter describes how to run a streaming audio service. Yes, you can run your own Internet radio station.
