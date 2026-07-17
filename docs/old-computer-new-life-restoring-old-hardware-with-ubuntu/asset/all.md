![](Images/cover.jpg)

![](Images/cover.jpg)

**Old Computer, New Life: Restoring Old Hardware With Ubuntu**

By: Stefan Neagu, [http://tuxgeek.me](http://tuxgeek.me)

Edited by Justin Pot

This manual is the intellectual property of MakeUseOf. It must only be published in its original form. Using parts or republishing altered parts of this guide is prohibited without permission from MakeUseOf.com

Think you’ve got what it takes to write a manual for MakeUseOf.com? We’re always willing to hear a pitch! Send your ideas to [justinpot@makeuseof.com](mailto:justinpot@makeuseof.com); you might earn up to $400.

# Table of Contents

[Introduction](../Text/chapter-1.xhtml)

[Preparation](../Text/chapter-2.xhtml)

[Installation](../Text/chapter-3.xhtml)

[Initial Configuration](../Text/chapter-4.xhtml)

[Further Configuration](../Text/chapter-5.xhtml)

[Overview of other distributions](../Text/chapter-6.xhtml)

[Conclusion](../Text/chapter-7.xhtml)

[MakeUseOf](../Text/chapter-8.xhtml)

# Introduction

The computer industry has evolved over the years more rapidly than any industry in contemporary history. Year after year engineers have worked valiantly to bring us, the end users, faster and more capable hardware without sacrificing reliability. Programmers and application developers have been equally quick to develop new software that puts to use the new hardware specifications.

However, while striving to sell more and more products, marketing departments want us to believe that PCs, laptops and netbooks become obsolete after a couple of years, and not replacing them makes us luddites.

It’s not true. Except for high-end gaming, a mid-level system bought in 2006 will provide enough functionality to get work done and have fun in 2011\. Word processing, Internet surfing, watching movies – either from DVDs or from your friends at the Pirate Bay - shouldn’t make your old system think twice, granted it is configured correctly, up-to-date and has a operating system that’s efficient, performance oriented, and free as in free beer and free speech.

## FLOSS every day

FLOSS is an abbreviation for **free/libre/open-source software**. Developers around the world contribute their work freely to different types of open source projects. Anyone with the required programming skills can see, use, and improve the code for the benefit of the entire community.

Examples of these kinds of projects include Mozilla Firefox, Chromium, the majority of Linux distributions (such as Ubuntu), VLC (a media player) and so on. There are literally thousands of applications that cost nothing and cover 90% of an average user’s needs in regards to computing in a modern software environment.

On a personal note, I get better frame rates (14-17 more frames per second) while running Need For Speed Carbon on an Ubuntu 7.04 machine from 2001 than on the same machine running Windows XP SP3\. This while running a piece of emulation software in the background which translates Win32 libraries necessary for DirectX acceleration, which [Ubuntu](http://www.makeuseof.com/tag/ubuntu-1104-unity-big-leap-linux/) doesn’t have.

Ironic, isn’t it? Thanks to FLOSS we can put that old computer to good use – with no financial investment on your part.

## Use Cases

So what are we going to do with your old PC? There are a few options available; depending on your configuration, computer skills and time you are willing to spend on the project. This guide covers the basic setup.

• **Desktop PC** – we can turn that old PC you use as a dust holder into a fully functional machine for browsing the web, email, chat, word processing, spreadsheets, movies and low end 3D games. At the most, you should only have to buy some extra RAM memory. It won’t take more than an afternoon and a couple of cups of coffee. All you have to do to achieve this functionality is to follow the instructions for installing the OS and the media packages provided in this guide.

• **Local file server/backup** – we can replace the old hard drive or attach an external one with a higher capacity and speed. With a wireless network card and some software, we can build a do it yourself version of [Apple’s Time Capsule](http://www.apple.com/timecapsule/). This sort of server can be used to centrally store all of your music, photos, and documents and make them available on the fly to any computer on the local network. You could even set up an FTP service in order to access your files when you are not at home. This can be a tad complicated, as it requires static IPs, command line input and knowing how to handle an FTP client. All you have to do is install SAMBA and configure it. Skip the media packages installation instructions.

• **Learning center for children** – there are hundreds of educational games available in the Ubuntu software repositories which makes it an excellent option if you have kids under 12\. They can learn math, history, geography and, thanks to the parental controls and advanced security inherent to Linux distributions, no need to worry about viruses, spyware and Internet stalkers. Follow the instructions provided, but skip the SAMBA installation. See the section titled “Educational Packages”

## What is Ubuntu?

Ubuntu is a Linux distribution supported officially by Canonical. The team at Canonical actively supports developers working on the operating system with money from donations and commercial activities like providing support and technical assistance for corporate clients.

It is the most popular Linux distribution, it benefits from a rapid release schedule, bug testing and a large supportive community at [ubuntuforums.org](http://ubuntuforums.org). As a FLOSS project, it too is available at no cost. Like any modern operating system, it supports a large variety of hardware and can serve as a primary operating system in a workplace environment as well as at home.

![](Images/1.jpg)

Above, Ubuntu Linux 11.04 (Natty Narwhal) is running in a virtual machine with specifications customized to resemble a low end PC. As it is a widely used, multi-purpose, efficient OS, Ubuntu serves as an ideal building block for our customized PC.

Ubuntu comes pre-installed with a range of [software](http://www.makeuseof.com/tag/5-tips-tricks-ubuntu-software-center-linux/): LibreOffice (OpenOffice in versions prior to 11.04), Firefox, Empathy (Pidgin in versions before 9.10), Transmission, GIMP (in versions prior to 10.04), and several lightweight games (such as Sudoku and chess). For additional packages, I’ll show you how to use the Synaptic Package Manager.

The minimum hardware requirements are:

• Server version – Processor x86 platform at 300Mhz; 128MB of RAM, 1 GB free space on the hard drive and a monitor with a minimum resolution of 640x480.

• Desktop version – Processor x86 platform at 1Ghz; 384MB of RAM, 5GB free space on the hard drive and a monitor with a minimum resolution of 1024x768.

Which in layman’s terms means that any new computer bought after 2002 will work just fine. While all the graphic whizzbang might not work (the Unity desktop theme, 3D compositing, High Definition videos, video streaming) you will be able to do all the basic tasks.

## How will Ubuntu give the computer new life?

**Ubuntu is efficient**

Linux distributions come from decades long experience in server rooms, and if there’s something that system administrators appreciate in an OS (operating system), it’s efficiency: sleek, lean code that gets the job done without wasting CPU (central processing unit) cycles. Even five seconds more from the bootloader (a small application that initializes the OS at boot) to the window manager is something that sys admins are not ready to put up with. Coming from such a harsh and demanding environment has made Linux distributions the best in their class.

Simply put: Linux in general and Ubuntu specifically, is great at making old computers seem new because it makes better use of the hardware on your PC. It is designed to get the job done in the most efficient way, with the least possible strain on the hardware resources as humanly possible. I say humanly possible because there is a programming principle that dictates that a compromise must be made between [portability of the code](http://en.wikipedia.org/wiki/C_(programming_language)%23Uses) and overall efficiency. This is the main reason for choosing Ubuntu as a platform for this project.

**Ubuntu is customizable**

Ubuntu allows its users to easily [customize](http://www.makeuseof.com/tag/6-handy-sites-learn-ubuntu-tweaks-tricks/) every aspect about the machine’s functionality.

**Ubuntu doesn’t require an investment**

It’s easy enough to use that you don’t need to spend money on training courses or books. 99% of applications designed for it are completely free of charge.

**In the other camp**

Developers at Microsoft don’t have the whole developer community bearing down and poking at their code – pointing out flaws – there is less accountability, because only the specific team working on the project can see and modify the source code. Plus, as their main market products are aimed at end-user consumers, they don’t stand for the efficiency principle REQUIRED in server rooms, where Linux is at home.

**Linux is a modular operating system**

Considering the wealth of options available from both the perspective of operating systems and software, you can customize a machine that is specifically designed to suit your needs – remote video monitoring, food recipe database, a control panel for an awesome laser projector that changes intensity in sync with the beat of music; you can build whatever you want.

A testament to the modular design of Linux is that a variant of Red Hat Linux is used to control the electro-magnets inside the Large Hadron Collider. As an OS, Ubuntu is small building blocks amounting to a whole. Even if it is not covered in this guide, you can use the old machine to [perform any tasks](http://www.makeuseof.com/tag/6-fun-ways-explore-ubuntu-1010-linux/) you can think of. It’s up to you to research niche software that serves your purpose.

This ability to add and drop functionality according to your use case is another point for efficiency, what is needed for old hardware.

# Preparation

## Backing up

Before we get to the good stuff, we need to do some preparation work. Although you’re probably no longer using the system, you should open it and search for documents, videos, photos, music that you haven’t got around to backing up. Be cautious and check twice, because we’ll need to erase everything from the hard drive later on.

Backing up is not a difficult task to achieve although it may be tedious if you have lots of data scattered around on that old hard drive.

The easiest way to save your files is to plug in the USB port at the back of the computer an [external hard drive](http://en.wikipedia.org/wiki/External_hard_drive%23External_removable_drives).

1\. Double clicking on the My Computer icon on the Desktop or in the Start menu will reveal a window which contains the file tree of the external hard drive.

2\. Find and copy the necessary files by selecting them and tapping Ctrl+C, activating the external hard disk file tree by clicking inside the window we opened earlier, and tapping Ctrl+V. Alternatively, you can select the files and drag’n’drop them into the external hard drive window.

If you don’t own an external hard drive or a USB stick, you could use the CD/DVD burner and software such as CDBurnerXP or InfraBurner to safely store your files on optical media. MakeUseOf has articles on a range of [suitable software](http://www.makeuseof.com/tag/the-best-free-alternatives-to-nero-cddvd-burner/). If you don’t know how to burn your files to a disk, MakeUseOf has an article [explaining all the steps for ImgBurn](http://www.makeuseof.com/tag/imgburn-easy-free-cd-and-dvd-burner-app/).

If you have software that [automatically backs up your data](http://www.makeuseof.com/tag/what-do-you-get-if-you-combine-dropbox-and-mozy-wuala/) to the cloud, such as Mozy or Dropbox, all you need to do is connect the computer to the Internet and wait for the application to complete the syncing process. Depending on the number and size of the files, it may take a while; be patient.

## Checking your specifications

Knowing a little about the hardware inside your computer is important later on if there are compatibility issues. It is important that you write these down now because if something breaks during the installation process or at first boot, you will need to search the various forums of the Ubuntu community for a driver, kernel patch or package.

![](Images/2.jpg)

We don’t need to write down all of the hardware specifications because drivers for things such as Ethernet cards are 99.99% of the time compatible. Bluetooth chips, card readers and printers are trickier but most of them are supported as well by default. Even if, let’s say, you have a very rare Ethernet card, we can just use the System Profiler tool to discover the specifications after we’re done installing the operating system.

If you’re running Windows, msinfo32 is a small program included with Windows 2000, Me, XP and later versions of Windows. This program gives you a comprehensive view of all the hardware present in your system.

1\. Click Start and Run.

2\. Type **msinfo32** and press enter.

For Windows 7 and Windows Vista, follow these steps:

1\. Click the Start button then choose the Control Panel.

2\. Click the System and Security link from this window.

3\. The System and Security window opens up and you can see the link for the Device Manager.

MakeUseOf Manuals author Lachlan Roy has written an extensive guide explaining the ins and outs of hardware. I strongly recommend you [download and read it](http://www.makeuseof.com/tag/pc-hardware-guide-download/). It should go a long way to helping you better understand what’s „under the hood’ of your machine.

## Getting Ubuntu

The easiest and most convenient way to get Ubuntu is to download the .ISO image file, which is available at Ubuntu.com or from mirror servers in countries around the world. While downloading from the Canonical server is straightforward, downloading from a mirror is faster.

For example, I use [the mirror](http://ftp.roedu.net/mirrors/ubuntulinux.org/) provided by a student union in my country which has a speed of around 1.2MB/s.

1\. Open your web browser and click on [this link](http://www.ubuntu.com/download/ubuntu/download). There should be a red button indicating “Ubuntu 11.04 32-bit”. That is the version we’re looking for. A few months from the publishing of this guide, the version number will change to look something along the lines of “Ubuntu XX.0X 32-bit”. It’s okay, this should work just as well (in theory).

2\. Alternatively, open up Google and search for “ubuntu mirror” + “name-of- your-country”. Download the latest version available, by looking at the right column of the FTP table which contains the file timestamp. You need a file that has this sort of filename “ubuntu-XX.0X-desktop-i386.iso” where the XX.0X represents the version number.

3\. Click on Start Download and save the file if requested.

After downloading the image file we need to burn it onto a CD or create a bootable USB stick. To burn an image CD, we’re going to use one of my favorite pieces of software, ImgBurn.

1\. Download ImgBurn by clicking the [Download button on this page](http://www.softpedia.com/get/CD-DVD-Tools/Data-CD-DVD-Burning/ImgBurn.shtml), available courtesy of Softpedia.

2\. Install and open ImgBurn.

3\. Select “Write Image File to Disk” and choose the file we downloaded earlier.

4\. Insert a blank CD and click on “Burn”.

To create a bootable USB stick, follow these steps:

1\. Download “USB Installer” by following [this link](http://www.pendrivelinux.com/downloads/Universal-USB-Installer/Universal-USB-Installer.exe).

2\. Select Ubuntu 11.04 (or another appropriate version depending on your time of reading) from the dropdown list.

3\. Select the image file we downloaded earlier.

4\. Go to My Computer and locate the drive letter corresponding to the USB drive (ex.: K:, G:, etc.) then select the correct drive letter from the dropdown menu in ImgBurn.

5\. Click on Create and wait for the process to finish.

Now that we’ve successfully created our installation media, we need to find out how to boot from it. It differs from computer to computer, but if you pay attention closely when you turn on your computer, there should be a BIOS message appearing shortly on the screen that says something like “Press F12 now to boot from alternative media” or “Press DEL to run Setup”. If you don’t know how to boot from a CD or a USB drive, Hiren.info has a [complete guide](http://www.hiren.info/pages/bios-boot-cdrom) for most of the BIOS manufacturers.

**Important**: Make sure you’ve backed up ALL YOUR DATA before proceeding further. We are going to format the entire hard drive, which means all data not backed up will be **PERMANENTLY LOST**.

# Installation

Installing a Linux distribution used to be an insipid task back in the day (believe me, you don’t want to spend Saturday nights compiling the kernel) but it has become easier over the years. In many respects, it’s easier to install Ubuntu than any modern version of Windows.

1\. Insert the CD or USB stick containing the OS image we’ve burned earlier.

2\. Shut down and then turn on your computer.

3\. Boot from the installation media, either the CD or USB stick.

**Step 1**: Select your language from the panel on the left side, then click on the “Install Ubuntu” button on the right.

![](Images/3.jpg)

**Step 2**: At the “Preparing to install Ubuntu” window, make sure all the requirements have green check arrows next to them. If you don’t have Internet connectivity yet, don’t panic, it’s not imperative.

Make sure the option to “install this third party software” at the bottom of the window is selected. It will ensure that Ubuntu will be able to play MP3 music files out of the box. If you have an Internet connection, also check the “Download updates while installing” checkbox.

![](Images/4.jpg)

**Step 3**: At the next screen, choose the third option in the list called “Erase everything and reinstall”. It will **format the hard drive** using the ext4 filesystem – allowing us to start from scratch with all the hard drive capacity available to the OS.

![](Images/5.jpg)

**Step 3***: If Ubuntu can’t detect your keyboard layout, you will be asked to manually do so. If you know the type of keyboard layout you have, select it from the list and click “Forward”. If not, just leave the default choice selected and click “Forward”.

**Step 4**: At the next window, enter the requested information, such as your name, account username and password. You will need your username and password later on – so make sure you write them down and keep them in a safe place.

![](Images/6.jpg)

**Step 4***: If you want to store sensitive information such as work documents, passwords, bank account information and your system has more than 512MB of RAM and a processor with at least a clock speed of 1,5Ghz, also select the checkbox named “Encrypt my home folder”.

Use the [GRC password creator](https://www.grc.com/passwords.htm) in order to obtain a high-strength passphrase. Use the third field, and select a password at least 16 characters in length.

![](Images/7.jpg)

**Step 5**: You’re almost done, congratulations. All you need to do now is select the time zone specific to your geographic location. In my case, it’s GMT+2 Bucharest.

![](Images/8.jpg)

**Step 6**: Let the installer complete, and then restart your computer when prompted to do so. Make sure that all installation media is removed from the computer before restarting. A message will appear on the screen at the appropriate time to do so.

# Initial configuration

Note: There is a small chance that your system will have enough horse-power to run the Unity 3D user interface. This means that your hardware is relatively new. Instructions provided in this guide are aimed at low-end PCs which will only be compatible with the default window manager and Unity 2D. This is how Unity 3D looks:

![](Images/9.jpg)

This is a screenshot of Unity 3D running on Ubuntu 11.04 courtesy of [WebUpd8](http://www.webupd8.org/). Later in this guide, I will provide instructions on how to install and enable the Unity 2D, less resource-intensive version of this UI (user interface).

The following instructions are based on the assumption that your hardware is old – the premise of this guide as stated in the title and introduction.

## First steps

Unlike Windows, Ubuntu comes pre-installed with a bunch of [software](http://www.makeuseof.com/pages/best-linux-software) that covers all the basic needs of a computer user. This is a great time to familiarize yourself with the desktop, user interface and applications.

![](Images/10.jpg)

**Main Menu**: On the upper left side of the screen you will see three menus and the Firefox icon. Select “Applications” and look around. All of them were written with ease of use in mind, and many have interfaces that closely resemble their closed source counterparts. For example, Empathy – the chat application – was made to resemble an earlier version of Yahoo! Messenger. It however has a cleaner, more intuitive UI and supports multiple protocols: Google Chat, Facebook, Yahoo! Messenger, Jabber, AIM and more.

![](Images/11.jpg)

**Notification Area**: On the upper right side of the screen you’ll see some icons, the clock, your username and the Shutdown button. Hover with your mouse above each icon and discover additional information provided to you by the system.

For example, the diverging arrows icon represents Connectivity; if there are network cards present in the system, they should appear here. The default nomenclature is “eth%” for Ethernet cards and “ath%” for wireless network cards. If a wireless connection is present, a dialog box will appear automatically requesting you to choose a WiFi access point and input a password (if the network is protected).

If you configured Empathy earlier with your chat credentials, the bubble next to your username will visually confirm your availability. In my case, it shows an X, for “signed out” or offline.

![](Images/12.jpg)

**Folders and window bar**: Select Places from the main menu at the top, then click on Home Folder. This is where you store all your files – they are equivalents to My Documents, My Photos and so on from Windows.

At the bottom of the screen, notice a new rectangle showing your username. This is the equivalent to the taskbar. Every new window you open will appear down there and you can select it with your mouse to bring focus to it.

On the right, there are four smaller rectangles; they represent workspaces – like having four virtual monitors. You can use one for all your work related windows, one for Facebook and chat, one for the music player and so on. The last icon in the bar is the Trash.

## Installing updates and extra packages

There are two ways of installing [applications](http://www.makeuseof.com/tag/repositories-package-management-ubuntu/) on your Ubuntu machine: using the graphical user interface and using the command line (the Terminal). I will illustrate both methods, so you can familiarize yourself with each.

We’re going to need Internet connectivity for the next section. If the wireless card doesn’t work, try connecting using the Ethernet port directly to your router. In 99% of configurations it is set up to connect automatically to your computer using DHCP and then to the Internet with no hassle on your part.

If that’s not available to you, try using a USB wireless network adapter. If you don’t have one, borrow one from a friend. This guide contains a Troubleshooting section which will help you fix the WiFi card problem – but you still need a temporary way to access the Internet.

**Installing updates:**

Making sure all of your software is up to date is a matter of going to System>Administration>Update Manager and clicking on Install Updates. Not only will it update system files and system utilities, but all of the installed software, like the LibreOffice word processor and Empathy.

![](Images/13.jpg)

Alternatively, open the Terminal and type in “sudo apt-get update” followed by “sudo apt-get upgrade” to achieve the same task.

**Installing extras:**

Go to Applications>Ubuntu Software Center.

![](Images/14.jpg)

Select the search box from the right corner and type in the package name. In this case “ubuntu-restricted-extras”. Select the package and click Install.

The package “ubuntu-restricted-extras” is a collection of commonly installed applications (such as Adobe’s Flash Player, and Microsoft’s TrueType fonts, Java Virtual Machine, support for RAR archives) that can’t be included in the default Ubuntu installation because of legal restrictions. Installing the same batch of applications on a Windows computer would have taken half an hour at best.

The process I described earlier works for any package you might need, just search for the name given to you in the tutorial or that a friend told you about.

Using the command line to achieve the same task is straightforward. Go to Applications>Accessories>Terminal. Type “sudo apt-get install ubuntu-restricted- extras” and press Enter.

## Repository bonanza

By default, Ubuntu 11.04 will try to run the 3D Unity theme. While it is more pleasing for the eye, it consumes resources.

You can get Unity without the 3D, though. To install Unity 2D, open Ubuntu Software Center and search for “unity 2d”. Select the package and click Install. If it doesn’t appear in the list, you don’t have the necessary repositories installed. Use the method described in Step 1*.

Go to Applications>Accessories>Terminal. Then type “sudo add-apt-repository ppa:unity-2d-team/unity-2d-daily” which provide the system with the location of the package. Type “sudo apt-get update” to update all of your software and repository lists.

Finally type in “sudo apt-get install unity-qt-default-settings” to complete the installation. Then log out. In the login screen, you will see “Unity Qt” in a drop-down menu. Pick that and login again.

Example terminal window command:

![](Images/15.jpg)

**Simple Preferences Management**

Ubuntu Tweak is a small application that takes all the hard work out of configuring advanced system settings, cleaning up, and installing other nifty packages.

At the command prompt type in “sudo add-apt-repository ppa:tualatrix/ppa” and press Enter; that command instructed the apt daemon where it could search for this additional software. Type in “sudo apt-get update” and press Enter; this makes sure all of your packages are up-to-date. Type in “sudo apt-get install ubuntu-tweak” and press Enter; this last command fetches the required files and installs the application.

![](Images/16.jpg)

Explore the software and you’ll find a variety of tweaks. For example: go to Applications>System Utilities>Ubuntu Tweak. Click on the Source Center>File Sharing>Transmission Stable builds checkbox>Sync. Transmission is the premier Torrent and Magnet client, and is not available in the default repositories.

We just added the repository and installed Transmission in a few clicks – no command line necessary or scouting for repository links.

**Media compatibility**

“Medibuntu is a packaging project dedicated to distributing software that cannot be included in Ubuntu for various reasons, related to geographical variations in legislation regarding intellectual property, security and other issues.” Medibuntu contains non-free codecs (like WMV) and support for encrypted AAC files (songs purchased on iTunes).

To install this repository, open the Terminal and type in “sudo wget --output- document=/etc/apt/sources.list.d/medibuntu.list http://www.medibuntu.org/sources.list.d/$(lsb_release -cs).list &&sudo apt-get --quiet update && sudo apt-get --yes --quiet --allow-unauthenticated install medibuntu-keyring && sudo apt-get --quiet update” and press Enter.

**Movies**: This step only applies if you’re going to use the machine to play movies. If you want to set up a file server, skip this.

In the Terminal type “sudo apt-get install vlc”, press Enter; type in “sudo apt-get install non-free-codecs libxine1-ffmpeg gxine mencoder libmpcdec3 libquicktime1 flac faac faad sox ffmpeg2theora libmpeg2-4uudeview flac libmpeg3-1 mpeg3-utils mpegdemux liba52-dev mpeg2dec vorbis-tools id3v2 mpg321 mpg123 libflac++6 ffmpeg libmp4v2-0totem-mozilla icedax tagtool easytag id3tool lame nautilus-script- audio-convert libmad0 libjpeg-progs”.

For DVD support type in “sudo apt-get install libdvdcss2 && sudo /usr/share/doc/libdvdread4/./install-css.sh” and press Enter.

This step downloads and installs software that will enable you to enjoy all kinds of entertainment such as movies and music.

**Additional software**

Open the Ubuntu Software Center and search for Samba, Deja dup, Skype. Select each package as you find it and click install. Below are the command line inputs for the Terminal method of installation.

**Samba**: Sharing files with other Windows computers in a local network is made easy by Samba. In the Terminal, type in “sudo apt-get install samba” and press Enter. I’ll show you how to use Samba later on in this guide. We also need “sudo apt-get install system-config-samba”, as a graphical interface to the SMB daemon.

**Backup**: If you’re going to use this machine as a work station, you’ll want your files to be backed up automatically. The easiest way to do that is Deja-Dup. In the Terminal type in “sudo apt-get install deja-dup”. I’ll show you how to use it later on in this guide.

**Skype**: If you’ve used Skype on Windows, I’m sure you’ll want the same functionality on your Ubuntu box. In the Terminal type in “sudo apt-get update && sudo apt-get install skype“.

It installs a popular VOiP application called Skype. You can talk to other people who have Skype or call phones from your PC.

# Further configuration

## Solving hardware compatibility issues

Since the FLOSS community is dispersed and not centrally organized by design, sometimes hardware manufacturers choose to turn a blind eye to the needs of this growing community. An increasing number of proprietary drivers are made available to users for easy installation in the “Additional Drivers” tool. You can access it by going to System>Administration>Additional Drivers.

This tool will automatically check the vendor and product ID in an effort to locate the proprietary driver for you. These drivers can’t be installed by default due to legal restrictions, but you can install them manually.

![](Images/17.jpg)

If a driver is available for you, it will appear like in the screenshot above. A button labelled “Enable” will be shown in the lower right side of the window. Select the checkboxes next to the drivers you wish to enable then click on the “Enable” button. Installation will proceed with no further interaction on your part required.

For WiFi cards, the most common cause of headaches and nights spent reading forum posts, there is a tool called ndiswrapper. This tool manages to translate driver files (.sys/.inf) that were written for Windows, to be compatible with Ubuntu.

![](Images/18.jpg)

1\. Download and install the package called “ndisgtk” using the Ubuntu Software Center.

2\. Go to System>Administration>Windows Wireless Drivers or open a Terminal window and type in “sudo ndiskgtk”.

3\. Search Google for “Brand Name” + “Model Number” + “inf” + “file” + “driver” + “Windows XP”. Download the inf file and input the location in the ndiswrapper window. If the initial Google search doesn’t lead you to an inf file that works, search using an alternative OS, like “Windows Vista”, or omit “driver”/”file” from the query.

4\. It should work now. Go to System>Preferences>Network Connections and check the Wireless tab. (Mine doesn’t show anything in there because my virtual machine doesn’t have a WiFi card)

If ndiswrapper doesn’t work, you’ll have to find the source code to a driver created by the community (thus unsupported by the manufacturer) and compile the code. This process differs from card to card, and there are guides showing you how to do this in relation to a specific model or chipset. In most cases, you’ll also need new kernel headers.

I’ve been using Linux boxes for 6 years and I still find this process cumbersome and borderline impossible for a newbie to work out. An example command for the Atheros ath2k series of chipsets is as follows:

“wget http://snapshots.madwifi.org/madwifi-hal-0.10.5.6/madwifi-hal-0.10.5.6-r3835- 20080801.tar.gz tar -xvf madwifi-hal-0.10.5.6-r3835-20080801.tar.gz cd madwifi-hal- 0.10.5.6-r3835-20080801 sudo apt-get install build-essential linux-headers-$(uname -r) sudo make sudo make install”

Now consider that all of those version numbers are specific for a chipset series and not interchangeable. Your best option is to use this search in Google “site:ubuntuforums.org BRAND MODEL NUMBER driver” and hope someone has hacked together a driver and a guide for compiling it.

## Purchasing additional hardware

When buying new hardware, check the back of the box for Ubuntu compatibility and search the [Linux hardware compatibility list](http://linuxhcl.com/) and [Ubuntu Certified hardware list](http://www.ubuntu.com/certification/). You might need to buy additional RAM if you have a system with less than 512MB and want to use resource intensive applications. Any RAM that is compatible with your motherboard will work in Ubuntu.

Additional networking equipment must be checked first for compatibility, I cannot stress this enough. For a file server, you might need to buy an Ethernet card or a WiFi adapter.

## Configuring SAMBA shares

For file-sharing, file server

SAMBA is a tool that will let you access files from your Ubuntu box on Windows and Macintosh PCs, and vice versa. Go to System>Administration>Samba. Click on the Plus icon and select the directory you wish to share. I recommend creating a folder called a Dropbox, which is accessible to everyone in the network and writeable. Then use specific settings for folders like Documents and so on.

![](Images/19.jpg)

This way you will always be able to quickly back up a file to your Ubuntu box. In the Access panel select “Everyone”. Folders shared using the SAMBA client will appear in My Network Places, Network, or the equivalent on your operating system. This is basically a „do it yourself’ file server.

You can use your Ubuntu box as a backup drive for your other computers. For each computer you will need to create a separate visible, writeable, “everyone” folder and point your backup software to use it. If you have a WiFi network set up you’ve got yourself a poor man’s version of Apple’s Time Capsule.

## Backing up

For desktop PC, educational PC

Backing up data is essential, especially when you’re running on old hardware. Open Applications>System Tools>Deja Dup. Alternatively, open the Terminal and type “sudo deja-dup”.

![](Images/20.jpg)

Click on “Back Up...” then select the method you want to use from the drop down menu. Deja dup has integrated support for Amazon S3 and Rackspace Cloud Storage, if you want to back up to an offsite location. Otherwise, select the location of the external hard drive, FTP server, or Windows share.

If you have a SMB compatible router, connecting a hard drive to the USB port in the back will allow you to use that as the Deja dup backup drive. The checkbox for data encryption is selected by default, so your data is protected from prying eyes.

## Configuring the Firewall

Ubuntu comes preinstalled with a Firewall, which protects the system automatically from remote users that want to gain access. The graphical configuration utility for it needs to be downloaded manually.

Open up the Ubuntu Software Center and search for “firewall”; install the package called “Firewall Configuration”. Alternatively, open the Terminal and type in “sudo apt-get gufw”, then “sudo gufw” to start the configuration utility.

To start the configuration utility from the GUI, go to System>Administration>Firewall Configuration.

![](Images/21.jpg)

Just like any firewall, ufw allows us to create rules for applications and specific ports. Unlike using the command line, gufw allows simple intuitive input of rules.

## Power management

Whether you’re going to use the system as a file server or desktop PC, you need to configure your power settings. Go to System>Administration>Power Management.

If you want your file server to be always available, make sure the “Put the computer to sleep when inactive for:” is set to never. You might also want to consider buying an UPS (uninterruptible power supply) to make sure data isn’t corrupted if a power outage or surge occurs. The ext4 file system (default choice for Ubuntu 11.04), is very robust and can recover from such events as a whole, corrupting just files in the process of writing at the time of the event.

![](Images/22.jpg)

For a laptop or desktop PC, consider changing the sleep setting to somewhere around 10-30 minutes. You can also enable the “Spin down hard disks when possible”, because it will save power – essential for a laptop.

## Remote Torrent downloads

For Desktop PC and File Server

You can use the integrated web server in Transmission to download and manage transfers from another computer on the network (eg. download a torrent directly to your Ubuntu box from your Mac laptop).

Go to Applications>Internet>Transmission>Edit>Preferences>Web. Click the “Enable web client” check box. Click the “Use authentication” checkbox and select a username and password.

On any machine on your local network you can now open a web browser and direct it to:
http://ip_address_of_machine_running_transmission:9091/ to access the interface.

If your Ubuntu box is a file server, make sure you set up the Transmission download folder to be shared on the network, like I showed you. Then you can stream the downloads onto any computer on the network.

## Educational Packages

For Educational PC

While you might not find any use in the old hardware, your children might benefit from a selection of educational software made available for free in bundles according to age groups, thanks to the valiant efforts of the team behind Edubuntu, a Linux distribution based on Ubuntu, whose target audience are children under eighteen.

![](Images/23.jpg)

You can download and install these packages by opening the Ubuntu Software center and searching for the text highlighted in blue below. Or open a Terminal window and typing “sudo apt-get install” followed by:

**ubuntu-edu-preschool** - Preschool ( < 5 years old) educational application bundle

**ubuntu-edu-primary** - Primary ( ages 6-12) educational application bundle

**ubuntu-edu-secondary** - Secondary ( ages 13-18) educational application bundle

**ubuntu-edu-tertiary** - Tertiary ( university level ) educational application bundle

MakeUseOf [has an article](http://www.makeuseof.com/tag/4-childrens-linux-applications-to-keep-your-kids-ahead-of-the-game/) covering a few of these applications, if you’re not sure whether to install the edu packages or not.

# Overview of other distributions

Once you’re comfortable using Ubuntu you can take a look at alternative distributions. Each has a specific set of advantages and caveats.

**Lubuntu** - created by a team of Taiwanese and French developers, Lubuntu was designed to be as lightweight as possible. The main difference between it and Ubuntu is the window manager, LXDE (Lightweight X11 Desktop Environment). It comes pre-installed with AbiWord instead of LibreOffice.

**Xubuntu** – with its origins traced to the Isle Of Man, Xubuntu is yet another distribution based on the Ubuntu core. It uses Xfce, a relatively newer window manager also designed for low hardware requirements.

**Joli OS** – based on Ubuntu and Debian, Joli OS is fast and the most user friendly of the bunch. Intended as a netbook OS, it has a “heavy orientation towards web applications and services”, integrated online backup, it comes pre-installed with a variety of non-free codecs and integrates popular social networks like Facebook and Twitter within its interface.

**Peppermint** – taking off Debian and Ubuntu, Peppermint OS was designed with cloud computing in mind, integrating by default Mozilla’s Prism technology – making web apps appear as local. It’s easy on hardware because it is primarily inteded for netbooks.

**Frugalware Linux** – is a Slackware variant which employs the Blackbox window environment. By its Slackware origins I can tell you that it’s fast, robust but harder to operate.

You can find more distributions and relevant information about each one on [DistroWatch.org](http://distrowatch.com/).

# Conclusion

The possibilities are only restricted to the time you’re willing to spend searching for packages and reading documentation. The beauty of FLOSS is that there are no restrictions, you can always pick up someone else’s work and improve on it – “scratching your own itch” as Richard Stallman put it.

Others like you may benefit, be grateful and in turn learn and develop your work into something that “sometimes works” (from a python script I used a couple of years back).

*Let me take you for a ride With the devil in the details We'll kiss and tremble with delight* -Placebo

This guide was made possible with information gathered from various sources: DistroWatch.com, UnixMen.com, blog.sudobits.com, ubuntuforums.org, canonical.com

# MakeUseOf

Did you like this PDF Guide? Then why not visit MakeUseOf.com for daily posts on cool websites, free software and internet tips.

If you want more great guides like this, why not subscribe to MakeUseOf and receive instant access to 20+ PDF Guides like this one covering wide range of topics. Moreover, you will be able to download free Cheat Sheets, Free Giveaways and other cool things.

Home: [http://www.makeuseof.com](http://www.makeuseof.com)
MakeUseOf Directory: [http://www.makeuseof.com/dir](http://www.makeuseof.com/dir)
MakeUseOf Answers: [http://www.makeuseof.com/answers](http://www.makeuseof.com/answers)
Geeky Fun: [http://www.makeuseof.com/tech-fun](http://www.makeuseof.com/tech-fun)
PDF Guides: [http://www.makeuseof.com/pages/](http://www.makeuseof.com/pages/)
Tech Deals: [http://www.makeuseof.com/pages/hot-tech-deals](http://www.makeuseof.com/pages/hot-tech-deals)

Follow MakeUseOf:

RSS Feed: [http://feedproxy.google.com/Makeuseof](http://feedproxy.google.com/Makeuseof)
Newsletter: [http://www.makeuseof.com/pages/subscribe](http://www.makeuseof.com/pages/subscribe-to-makeuseof-newsletter)
Facebook: [http://www.facebook.com/makeuseof](http://www.facebook.com/makeuseof)
Twitter: [http://www.twitter.com/Makeuseof](http://www.twitter.com/Makeuseof)

Think you’ve got what it takes to write a manual for MakeUseOf.com? We’re always willing to hear a pitch! Send your ideas to [justinpot@makeuseof.com](mailto:justinpot@makeuseof.com); you might earn up to $400.