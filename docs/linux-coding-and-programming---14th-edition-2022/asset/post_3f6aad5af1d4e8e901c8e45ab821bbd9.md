
tools preinstalled, that a user can run for penetration testing against their network. There was once even a Hannah Montana Linux distribution but the less we talk about that the better. The point being, there’s a distro out there for you.

Needless to say, once you’ve mastered Linux to a relatively high degree, probably a power user ability, then you will want to expand your skills and begin to build your own Linux distro based on Arch, Debian or one of the many other distros available. Doing so involves a lot of command line knowledge, as well as knowledge on how the Linux system works and interacts with the hardware in the computer. You will need to partition your own hard drive, install a desktop environment and eventually install the apps and programs you want. Doing so takes time and again there are a lot of skills you’re going to need to learn.

Eventually you can consider yourself a technical Linux user but never consider yourself an expert, after all we’re always learning something new. You can build your own distro from scratch, help other Linux users out with problems, maybe even contribute to the improvement of a distro during its testing phase or build. Where next then?

Oddly enough, most higher-end technical users find themselves back at square one, using a distro like Linux Mint. The main reason is usually because it’s an easy option, and it’s a stable environment. Just because you know the system inside and out, doesn’t mean you always want to be fixing potential issues. Most of us would prefer the easy life, especially where technology is concerned, so the logical choice would be to choose a distro that’s simple, yet still powerful enough to do everything you want it to do, hence Linux Mint.

However, in the end, it’s purely down to choice, your own personal choice. You may find that after going through the tutorials in this title you don’t like Linux Mint or the Cinnamon desktop. Fine, you may prefer Ubuntu, Debian or openSUSE; that’s the beauty of Linux. The freedom to change what you want, to distro hop from one to another without being penalised by cost or lack of access.

The answer to the question, which distro is; any which one you like! It can be as complex or easy as you need it to be, as long as it does what you want it to do, then it’s perfect.

![](img/d501697c83491ed0bb4b382b0d28ef0a_16_0.png)

![](img/d501697c83491ed0bb4b382b0d28ef0a_16_1.png)

## Getting Started
## with Linux

> “In real open source, you have the right to control your own destiny.”
> — Linus Torvalds (developer of the Linux kernel)

![](img/d501697c83491ed0bb4b382b0d28ef0a_17_0.png)

### Getting Started with Linux

It’s all fine and well talking about how good Linux is but how do you get it on your computer? **Installing Linux** is remarkably simple but there are several options available to you. This section looks into how you can download the Linux ISO, install it on a PC as your main operating system and even how to install a virtual environment.

With a virtual environment you can run Linux while still using your main operating system, be that Windows or macOS. **Intrigued? Read on and find out more.**

- **20** Creating a Linux Installer on Windows
- **22** Installing Linux on a PC
- **24** Installing a Virtual Environment
- **26** Installing Linux in a Virtual Environment

### Creating a Linux Installer on Windows

You need to transfer the downloaded Linux ISO to either a DVD or a USB key before being able to install it onto a computer. This will be a live environment, which allows you to test the OS prior to installation, but first you need to create the bootable media.

### DVD BOOTABLE MEDIA

We’re using a Windows 10 PC here to transfer the ISO to a DVD. If you’re using a version of Windows from 7 onward the process is extremely easy.

- **STEP 1** First locate the ISO image of Linux you’ve already downloaded. You can usually find it in the Downloads folder in Windows 7, 8, 1 and 10 computers, unless you specified a different location when saving it.

![](img/d501697c83491ed0bb4b382b0d28ef0a_19_0.png)

![](img/d501697c83491ed0bb4b382b0d28ef0a_19_1.png)

- **STEP 3** Right-click the Linux ISO and from the menu select Burn Disc Image. Depending on the speed of the PC, it may take a few seconds before anything happens. Don’t worry too much, unless it takes more than a minute, in which case it might be worth restarting your PC and trying again. With luck, the Windows Disc Image Burner should launch.

![](img/d501697c83491ed0bb4b382b0d28ef0a_19_2.png)

![](img/d501697c83491ed0bb4b382b0d28ef0a_19_3.png)

- **STEP 2** Next insert a recordable DVD disc into your computer’s optical drive. After a few seconds, while the disc is read, Windows displays a pop-up message asking you what to do with the newly inserted disc. Ignore this, as we’re going to use the built-in image burning function.

- **STEP 4** With the Windows Disc Image Burner dialogue box open, then the ‘Verify disc after burning’ tick box, then the Burn button. The process should take a few minutes, depending on the speed of your PC’s optical drive. Once it’s complete it runs through the verification stage and when done the optical drive should auto-eject the disc for you.

![](img/d501697c83491ed0bb4b382b0d28ef0a_19_2.png)

![](img/d501697c83491ed0bb4b382b0d28ef0a_19_3.png)

### USB BOOTABLE MEDIA

USB media is faster than a DVD and often more convenient, as most modern PCs don't have an optical drive installed. The process of transferring the image is easy but you need a third-party app first and a USB flash drive of 4GB or more.

**STEP 1** First open up a web browser and go to www.rufus.akeo.ie/. Scroll down the page a little and you come to a Download heading, under which is the latest version of Rufus. Left click the link to start the download.

![](img/d501697c83491ed0bb4b382b0d28ef0a_20_0.png)

**STEP 2** Double-click the downloaded Rufus executable and click Yes to the Windows security question and Yes to checking for updates. With Rufus launched it should have already identified your inserted USB flash drive; if not, just remove and reinsert.

![](img/d501697c83491ed0bb4b382b0d28ef0a_20_1.png)

**STEP 3** At first glance the Rufus interface can look a little confusing but don't worry, it's really quite simple. To begin with, click on the SELECT button next to the 'Disk or ISO Image (Please select)' pull-down menu. This launches a Windows Explorer window where you can locate and select the Linux ISO.

![](img/d501697c83491ed0bb4b382b0d28ef0a_20_2.png)

**STEP 4** When you're ready, click on the Start button at the bottom of the Rufus app. This may open up another dialogue box asking you to download and use a new version of SysLinux. SysLinux is a selection of boot loaders, used to allow a modern PC to access and boot from a USB flash drive. It is necessary, so if asked click on 'Yes' to continue.

![](img/d501697c83491ed0bb4b382b0d28ef0a_20_3.png)

**STEP 5** The next step asks which image mode you want the Linux ISO to be written to the USB flash drive in. Both methods work for different situations but generally, the recommended ISO Image Mode is the more popular. Make sure this mode is preset and click OK to continue, followed by OK again to confirm the action.

![](img/d501697c83491ed0bb4b382b0d28ef0a_20_4.png)

**STEP 6** The Linux ISO is now transferred to the USB flash drive. The process shouldn't take too long, again depending on the speed of the USB device and the PC. You may find Rufus auto-opens the USB drive in Windows Explorer during the process; don't worry you can minimise or close it if you want. When the process is complete, click on the Close button.

![](img/d501697c83491ed0bb4b382b0d28ef0a_20_5.png)

### Installing Linux on a PC

Most Linux distros come as a Live Environment. This means you can boot into an actual, fully-working distro straight from the DVD or USB that you just created. Let’s see how that works and how you go about installing Linux from there.

### UEFI BIOS

The Unified Extensible Firmware Interface (UEFI) is used to identify hardware and protect a PC during its boot-up process. It replaces the traditional BIOS but can cause issues when installing Linux.

- **STEP 1** Insert your DVD or USB flash drive into your PC and, if you haven’t already, shutdown Windows. In this instance we’re using the USB boot media but the process is virtually identical. Start the PC and when prompted press the appropriate keys to enter the BIOS or SETUP, which could for example be: F2, Del or even F11.

![](img/d501697c83491ed0bb4b382b0d28ef0a_21_0.png)

![](img/d501697c83491ed0bb4b382b0d28ef0a_21_1.png)

- **STEP 3** With UEFI turned to Legacy mode, there are now two ways of booting into the Live Environment. The first is via the BIOS you’re already in. Locate the Boot Sequence and change the first boot device from its original setting, usually Internal HDD or similar, to: USB Storage Device for the USB media option, or DVD Drive for the DVD media option.

![](img/d501697c83491ed0bb4b382b0d28ef0a_21_2.png)

![](img/d501697c83491ed0bb4b382b0d28ef0a_21_3.png)

- **STEP 2** There are different versions of a UEFI BIOS, so covering them all would be impossible. What we’re looking for is a section that details the Boot Sequence or Boot Mode. Here you have the option to turn off UEFI and choose Legacy or Disable Secure Booting. Most distros work with UEFI but it can be a tricky process to enable it to boot.

- **STEP 4** Alternatively use the Boot Option Menu. With this option you can press F12 (or something similar) to display a list of boot media options; from there, you can choose the appropriate boot media. Either way, you can now Save and Exit the BIOS by navigating to the Save & Exit option and choosing ‘Save Changes and Exit’.
