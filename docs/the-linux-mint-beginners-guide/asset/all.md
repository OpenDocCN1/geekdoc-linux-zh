![](cover.jpg)

![cover](cover.jpg)

THE LINUX MINT BEGINNER'S GUIDE - SECOND EDITION

Jonathan Moeller

***

## Book Description

The Linux Mint Beginner's Guide will show you how to get the most out of Linux Mint, from using the Cinnamon desktop environment to advanced command-line tasks. In the Guide, you will learn how to:

-Install Linux Mint.

-Use the desktop environment.

-Manage files and folders.

-Manage users, groups, and file permissions.

-Install software on a Linux Mint system, both from the command line and the GUI.

-Configure network settings.

-Use the vi editor to edit system configuration files.

-Install and configure a Samba server for file sharing.

-Install SSH for remote system control using public key/private key encryption.

-Install a LAMP server.

-Install web applications like WordPress.

-Configure an FTP server.

-Manage ebooks.

-Convert digital media.

-And many other topics.

***

The Linux Mint Beginner's Guide

Copyright 2012 by Jonathan Moeller

Second Edition published August 2017

Cover image copyright andresr Imaging | istockphoto.com

Published by Azure Flame Media, LLC

All Rights Reserved.

Trademarked names may appear in this book. Rather than use a trademark symbol with every appearance of a trademarked name, this book uses the names only in an editorial fashion and to the benefit of the trademark owner, with no intention of infringement of the trademark.

The information in this book is distributed on an "as is" basis without warranty. Although every precaution has been taken in the preparation of this work, neither the author nor the publishers shall have any liability to any person or entity with respect to any loss or damage caused or alleged to be caused directly or indirectly by the information contained in this work.

***

## Introduction

Welcome to the second edition of “The Linux Mint Beginner's Guide”. If you are a new Linux Mint user, you've come to the right place. Linux Mint is a powerful and versatile modern operating system, and you can use its desktop edition to perform a wide variety of tasks, ranging from office work and Internet browsing to listening to music and playing games. In this book, we'll introduce you to the basics of using Linux Mint and working with its interface.

WHAT IS LINX MINT?

What exactly is “Linux Mint”, though?

“Linux” refers generally to a family of free operating systems based upon the Linux kernel (a kernel is the core component of any operating system). The history of Linux is long and complex, but we can provide a brief sketch here. In the late 1960s and 1970s, AT&T’s Bell Labs developed the UNIX operating system, which was soon used in university computer labs across the United States.

However, AT&T retained the rights to the UNIX code, which meant that people could not freely alter or distribute it. In response to this, computer programmer Richard Stallman launched the GNU Project in 1983\. (GNU stands for "GNU’s Not Unix.") Stallman’s goal with the GNU Project was to create a UNIX-like operating system that was nonetheless free to alter and distribute under the principle of “Free Software”, a philosophical position which argued that software should be free to distribute and alter without legal restrictions. The GNU Project and Stallman himself produced a large number of software tools and programs. Unfortunately, the GNU Project lacked a viable kernel, the necessary core of any operating system.

This changed in 1991 when a Finnish university student named Linus Torvald became frustrated with the academic licensing for Minix, a UNIX-like operating system restricted to educational use. Torvalds wrote his own kernel, named it Linux, and released it under the GNU free license. Combined with the GNU project, the Linux kernel provided a freely available operating system – an operating system that people could modify and distribute however they saw fit.

Linux had been born.

(Many people insist that the proper name of Linux should in fact be GNU\Linux, in recognition of GNU’s vital role, and many GNU programs are used in Linux to this day.)

Under the terms of GNU’s General Public License (GPL), anyone could modify and distribute Linux. Today, Linux and Linux variants run on every different computing platform, from smartphones to desktop computers to high-end server systems. (Even Amazon's Kindle and Barnes & Noble's Nook e-reader devices are powered by custom versions of Android, a version of Linux designed for smartphones and tablets.) These different flavors of Linux are called Linux “distributions.” Some distributions are commercially supported endeavors, like Red Hat Linux or SuSE Linux, while others are free and community-supported, like Knoppix or Fedora.

One of the more venerable distributions is Debian, started in 1993 by a German programmer named Ian Murdock. Debian is well-known for its stability and its strong devotion to free software principles. Unfortunately, Debian also has a famously slow release cycle. Because of this, Debian is frequently “forked” – a “fork” is when the code of an open-source project (which is free to share and distribute) is used as the foundation for another open-source project.

Linux Mint is derived from Ubuntu, one of these forks. Started by South African entrepreneur Mark Shuttleworth through his company Canonical, Ubuntu focused on providing a smooth experience for the end users, offering a version of Linux for people with little experience with Linux or even with computers in general.

Linux Mint began as a fork of Ubuntu in 2006, founded by a developer named Clement Lefebvre. As Ubuntu made some controversial design decisions in 2011 and 2012, more and more users began migrating to Linux Mint. Currently, Linux Mint is one of the most popular Linux desktop distributions, and releases a new update twice a year.

THE PURPOSE OF THIS BOOK

The purpose of this book is to give the reader a basic introduction to using the Linux Mint operating system. This book is not intending as a comprehensive overview, but as an introduction to Linux Mint – enough information to get you started and to get you comfortable using Linux. In this book, we'll focus first on using the graphical interface, and then the command line itself.

If you have more interest in learning the command line itself, you can check out my other book – THE LINUX COMMAND LINE BEGINNER'S GUIDE.

(As an aside, Linux Mint is closely based on Ubuntu, which means many of the command-line operations described in this book will also work on most versions of Ubuntu.)

ERRATA

I have done my best to make sure all the information in this book is accurate and timely, and tested every command and procedure described in the following chapters. However, I am only mortal, and undoubtedly I have made mistakes. If you notice any errors, you can email me at jmcontact @ jonathanmoeller.com to let me know. The advantage of ebooks over paper books is that ebooks are vastly easier to update and revise, and I can quickly introduce a revised and updated edition to correct any mistakes. (Another advantage of an ebook is that you can have it open on your computer screen as you work, rather than having to look down at a paper book on your desk.)

A NOTE ON SCREENSHOTS

Since Linux Mint is a graphical operating system, this book includes many screenshots to illustrate the descriptions of the graphical user interface. However, if you are using a grayscale eInk reader, the screenshots may not be easy to view. If you have difficulty viewing the screenshots, I suggest reading the book on a tablet device, or on a PC screen using an ebook reading application.

NOTES ON THE SECOND EDITION

After five years, I am pleased to issue the second edition of the Linux Mint Beginner's Guide! Several chapters have been added, dealing with ebooks, media, and gaming, and all the existing chapters have been updated.

***

## Chapter 1 – Installing and Upgrading Linux Mint

You can't use Linux Mint without first installing it on a computer, and in this chapter we'll show you how to install Linux Mint on the computer of your choice. Additionally, we'll also show you how to update Linux Mint after it has been installed. Both Linux Mint and the various software packages included with it are being continuously updated and improved, and updating makes certain you have the latest, greatest, and most secure versions of your software.

SYSTEM REQUIREMENTS

Before installing Linux Mint, make sure that your computer meets the system requirements. The term “system requirements” only means that Linux Mint requires computer hardware of a certain speed and storage capacity to run well. Fortunately, Linux Mint's system requirements are not demanding, and definitely lower than those of Microsoft Windows.

Linux Mint first requires a processor running at a speed of 700 megahertz or higher. (The “processor” is the main computing chip in a computer, and its speed refers to how many clock cycles of calculations it can perform per second.) Most processors manufactured since 2001 or so run at a speed of 1 gigahertz or higher, so only very old processors will not run Linux Mint.

Linux Mint also requires 512 megabytes of memory and 5 gigabytes of free hard drive space. “Memory” refers to the amount of information the computer can load into its working memory at any one time. (Since this kind of memory is technically called Random Access Memory, RAM is a common shorthand for the computer's working memory.) However, when the computer shuts down, the information in the memory is lost. To prevent this data loss, information that needs to be stored long-term is written upon the hard drive. Since hard drives are much cheaper to manufacture than RAM chips, hard drives can store much more information than RAM. Virtually every modern computer comes with more than 512 megabytes of RAM and 5 gigabytes of hard drive storage space; only computers older than nine or ten years will have smaller quantities of storage.

Linux Mint also requires a computer with a video adapter and a monitor capable of displaying a screen resolution of 1024 by 768 pixels. Again, most modern computers are capable of that. You might run into problems if your video adapter is incompatible with Linux Mint. Fortunately, you can test this using the LiveCD mode, which will discuss in the next section.

Finally, your computer needs either a CD-ROM drive or a USB port to install Linux Mint. You can install Linux Mint using either a CD-RW disc or a USB flash drive, and we'll discuss both methods.

USB OR CD?

To install Linux Mint, you'll first need to download the ISO file of Linux Mint, available at http://www.Linux Mint.com/download/desktop. (An “ISO file” is the term for an image file of a disk.) Once you have the ISO file, you can burn it to a CD, or prepare it on a USB flash drive for installation.

Burning to a CD is the most common method. Once you burn the Linux Mint ISO to a CD, you can then use that disc to boot up a computer with an optical drive and run the installer for Linux Mint. The advantage of this approach is that most computers have optical drives, and can therefore boot off a burned Linux Mint CD. The downside is that optical drives are comparatively loud and slow. In addition, on older computers, I've noticed that optical drives have a disturbing habit of breaking down when attempting to install Linux Mint.

Creating a bootable USB Linux Mint drive is a bit more work (to do so, download the installer from www.pendrivelinux.com), but it is has many advantages. First, a USB flash drive is usually faster and more reliable than a burned CD. Second, it's quieter than a CD drive, and it's far easier to carry a USB flash drive with you if you need to install Linux Mint on a regular basis. However, not all computers support booting from a USB flash drive, especially older computers. For those systems, you might have to use a CD.

INSTALLING Linux Mint

Once you have decided on a CD or a USB flash drive, you're ready to install Linux Mint.

Boot your computer using the CD or the flash drive. For some computers, you might have to hit a particular key when the manufacturer's logo flashes on the screen to access the boot menu. (For Dell computers, for instance, it's usually the F12 key, and on Asus computers it's often the ESC key.)

Once your computer has booted from the CD or the USB flash drive, you should see this screen:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_7af41301.jpg)

This screen lets you select your language, and also allows you to select between trying Linux Mint and installing Linux Mint. The “Try Linux Mint” button boots you into the full Linux Mint environment, running off the CD or the USB flash drive, with access to all of Linux Mint's included software. This is useful for troubleshooting (for instance, if you have a computer that will not boot), and it's also useful for testing before you install Linux Mint. This allows you to make sure that hardware such as your graphics adapter or wireless network card will work properly with Linux Mint.

For now, we'll focus on installing Linux Mint. Click on the “Install Linux Mint” button to begin the installation process. You will then see this screen:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_2df451cf.jpg)

This screen reminds you that you will need 4.4 gigabytes of free drive space (five is better) to install Linux Mint. It also reminds you to connect your Linux Mint system to the Internet for the installation. This isn't strictly necessary, but it does allow the installer to download the latest updates in the background while you install Linux Mint, which you can enable by checking the “Download updates” checkbox.

The second checkbox, the “Install this third-party software” one, allows Linux Mint to install various multimedia codecs. This will allow your Linux Mint system to play MP3 audio files. Once you have made your selection, click on the Next button to continue.

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m579d9e16.jpg)

The installer will then ask you how you want to configure your computer's hard drive for Linux Mint. What options you see here will depend upon how many hard drives your computer has, and whether or not you already have an operating system installed. Generally, you will have a choice between wiping your disk and installing Linux Mint, or splitting the disk between the previous operating system and your new installation of Linux Mint. (Advanced users can also select more complicated configuration options here.) For now, we'll assume that you want to wipe out your hard drive and install Linux Mint on the blank disk, so select the option to erase the disk and install Linux Mint. (Note that this will wipe out anything already on the disk.)

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_c7e977a.jpg)

You will then need to confirm your options before the installer continues – if you change your mind, you can always hit Back. However, after you hit the Install Now button, your disk will be erased and Linux Mint installed. Once you're ready, and you're sure you've made the right configuration choices, hit the Install Now button.

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_c7e977a.jpg)

The installer will begin installing Linux Mint in the background, but will still ask you some additional questions as it works. First, you'll need to select your time zone by clicking on the world map. Click Continue once you've selected the appropriate time zone.

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_27b32d38.jpg)

Next, you'll need to select your keyboard layout. Most of the readers of this book will use the English (US) keyboard layout, which is the default, but Linux Mint supports hundreds of different languages and keyboard layouts. Select the appropriate one from the list, and then hit Continue.

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m1fbb5afa.jpg)

The installer will then ask you to set up a user account and a hostname for your computer. First, type your full name into the “Your name” field. Linux Mint will use this when it needs to display your full name.

Below that, enter a name for your computer. Technically, this is called a “hostname”, which is the name your computer will use to identify itself on the network. It's often best to pick a hostname that is easy to remember. If you're part of an organization (such as your workplace), they might have a standard naming convention for hostnames.

After that, put a username into the “Pick a username” field. Generally, you can combine your first initial with your last name to produce a username – for instance, a woman named Caina Amalas would make a username called camalas.

Next, pick a password for your user account. You'll want to pick a strong password, since the default account created during a Linux Mint installation has administrative rights to the system, which means it can install and uninstall programs. A strong password includes a mixture of capital letters, numbers, and punctuation marks, and it at least ten characters long.

Below the password field is a radio button to let your Linux Mint computer log in automatically upon boot. Generally, this is a bad idea – it's always best to use a password to log into your computer for reasons of security. (Especially since the default account created during installation has administrative rights to the Linux Mint system.)

The final option is to encrypt your home folder. “Encrypting” a file means that the contents are scrambled and can only be read using a special mathematical key. If you encrypt your home folder, that means that only your user account will be able to access it.

Once you have finished the password and account options, hit the Continue button, and the installation will proceed.

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m59ea6d6c.jpg)

And at that point, you're done. The installer will finish in the background, and you can watch a slideshow displaying Linux Mint's various features.

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m68e5b9ff.jpg)

Once the installation is finished, hit the Restart Now button. Before the system reboots, it will tell you to remove your CD or USB drive. Once you do, remove the CD or USB drive and hit the ENTER key. Your system will then reboot and take you to the logon screen:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m26f765c3.jpg)

Select your newly made account and enter your password, and you will be taken to your new Linux Mint desktop.

UPDATING Linux Mint

Once you've installed Linux Mint, you will want to make sure that it is up to date with the latest software patches. Software patches close potential security holes in your software and often provide new features. In fact, after you've installed Linux Mint, the Update Manager application will run automatically for the first time.

To run the Update Manager yourself, follow this steps.

First click on the mintMenu, go to Administration, and click on Update Manager.

Update Manager will then launch, and immediately contact the Linux Mint repositories (in Linux, a “repository” is an online storage space for applications) for updates.

Update Manager will display a list of the available updates, and the combined size of all the updates. (On a new Linux Mint installation, this can often run in the hundreds of megabytes.) If you click on an individual update, and then click the triangle next to “Description of update”, you can see more detailed information about an individual update. Clicking on the Settings button will let you change Update Manager's settings. By default, Update Manager checks for updates daily, and informs you when new updates are available to install.

Once you are ready to install updates, click on the Install Updates button to continue:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_6bf812f5.jpg)

Update Manager will then ask for your password. This is a common event on Linux Mint – if you want to do something that will change the system, like installing a new program or updates, it will ask for the password of an administrative account. Since the account you created during the installation process is an administrative account, go ahead and enter that password, and then hit the Authenticate button.

Update Manager will download and install the available updates. Depending on the speed of your Internet connection, this might take some time, so be patient.

Once Update Manager is finished, you will have to restart your computer. Click on the Restart button to reboot your system, and once Linux Mint comes back up, your computer will be fully up to date.

***

## Chapter 2 - Using the Linux Mint Desktop Interface

Linux Mint is designed as a graphical operating system, which means you will spend a great deal of time using the desktop and the various graphical interface options. In this chapter we’ll give you a tour of the desktop, and show you how to use Nemo File Manager to perform common file tasks. Additionally, we’ll show you how to use mintMenu, Linux Mint’s system menu.

THE DESKTOP

When you boot up your Linux Mint machine and log in for the first time, you will see the Desktop, which will look something like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_3b330d1e.jpg)

Most of the important parts of the Desktop are along the bottom, in the area called the Panel. The button in the lower left-hand corner, the Menu, takes you to the mintMenu, Linux Mint’s integrated application launcher and search function. Any running programs will show up in the central area of the Panel. On the right of the Panel, you’ll see the current date and time, along with the notification area – any running programs that have the capability to leave notifications will do so here.

DESKTOP ICONS

By default, you will only see two icons (at first) on your Linux Mint desktop, the Computer icon and a shortcut to your home folder:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_49d8df1.jpg)

Double-clicking on the Home icon launches Nemo, Linux Mint’s modified version of the Nautilus file management program. We’ll discuss Home folders more later in this chapter. Double-clicking on the Computer icon launches Nemo with a high-level view of your computer. You can see all the installed hard drives on your computer, along with any removable disks. You can also create documents and folders for yourself on the Desktop.

THE MINTMENU

Click on the Menu button in the lower left-hand corner of your Desktop, and you will summon the mintMenu, which will look something like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_3afa29e4.jpg)

The mintMenu has three main columns. The left column contains shortcuts to some of the most commonly used functions on your system. You can access the Firefox web browser, Software Manager, the Terminal, the Nemo File Manager, and fine-tune settings for Cinnamon, Linux Mint’s desktop environment. You can also lock your computer, log out, and reboot your computer.

The central column is a listing of the categories of applications installed on your Linux Mint computer. Click on the Office category, for instance, and you will see a listing of all the office-related applications (such as the LibreOffice office suite) installed on your computer. The central column also contains Recent Files, which lists all the files you have accessed recently.

Finally, the right-column is context-dependent, which means it changes based upon what you have selected in the central column. As we mentioned above, click on the Office category in the central column, and the view in the right-hand column will change to show the available applications in the Office category.

The mintMenu also has a search box at the top. Enter a term in the search box, and mintMenu will search your installed applications for it. For instance, if you wanted to launch LibreOffice Writer and you didn’t want to bother with looking with the categories, type “writer” in the search box, and mintMenu will find it for you:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m86ab1a1.jpg)

THE PANEL

The Panel is the bar running down the bottom of your Desktop. Like the mintMenu, it can be divided roughly into three areas. The left area contains the button to launch the mintMenu and pinned application shortcuts:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_40ee6da5.jpg)

The green button directly to the right of the Menu button minimizes all running windows and takes you to the Desktop. Next to this button are three application shortcuts – one for the Firefox web browser, one for the Terminal, and one for Nemo File Manager.

The middle area of the Panel displays any currently running applications:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_6e29adce.jpg)

By clicking on the buttons for the running applications, you can switch between them as necessary. The buttons will also display additional information, depending upon the program. For example, LibreOffice Writer’s button will display the name of the current document, and Nemo File Manager will show the name of the directory it is currently browsing.

The right area of the panel is the notification area:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m715cbf8e.jpg)

The notification area displays the date and time, along with several other key pieces of information. If there are updates available for your Linux Mint system, they will show up here with a white shield icon. You can also see the status of your network connection, control the volume, and by clicking on the window icon on the far right-hand side, see all the applications currently running on your computer.

The notification area also lets you make changes to the Panel settings itself. Click on the upward-pointing arrow icon, and move the slider switch for Panel Edit Mode from Off to On. (It’s set to Off by default to prevent you from accidentally altering the panel with an errant click.) Once Panel Edit Mode is enabled, you can add new launchers to the Panel and change the behavior of the notification area.

LOCKING THE SCREEN

Locking your screen when you are away from your computer is one of the easiest steps you can take to keep both your Linux Mint system and the data it contains secure. When you lock your screen, the display goes black. When you tap a key or click the mouse, you will see the prompt to enter the password of the currently logged-in user, like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_1ddac990.jpg)

Once the screen is locked, only the currently logged-in user can unlock the computer by entering his or her password. Alternatively, another user can access the computer by clicking the Switch User button and entering his password, but only if that user has a valid user account on that computer.

The security benefits of locking your screen when you're away from your computer should be obvious. If you leave your screen unlocked, anyone could come along and access your files or alter your system's settings. Even worse, sensitive data could fall into the wrong hands – consider the disaster that could result if you left your bank information open in Firefox and someone unscrupulous happened to see your information.

By default, Linux Mint is configured to lock your screen whenever your computer is idle for ten minutes. However, if you need to get up and leave your computer, you probably don't have the time to wait for your computer to lock itself. You can manually lock your screen by hitting the CTRL+ALT+L keys simultaneously. When you do, your screen will go black, and will remain black until you tap a key or move your mouse. After a key is tapped or the mouse is clicked, you'll see the prompt to enter your password or switch users. Enter your password, and the screen will unlock.

You can adjust the automatic lock settings by going to the mintMenu, to the Preferences category, and clicking on the Brightness and Lock icon in the top row. This will open up the Brightness and Lock settings:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m3217ddbd.jpg)

From here you can adjust both the screen lock settings and how long your computer will be idle before shutting off the screen. The first drop-down menu, “Turn screen off when inactive”, governs how long Linux Mint will wait before shutting off the screen when your computer is idle.

The Lock slider button governs whether or not your computer will lock or not. Below that is another drop-down menu that determines when the screen turns off. By default, the screen will lock when the monitor shuts off. You can, however, set the screen to lock automatically some time after the monitor powers off. For instance, you can set your monitor to shut off after 15 minutes, and the screen to lock after 30 minutes. (This would be useful if you spend a great deal of time in front of your computer while only using it intermittently – if you have to make numerous phone calls, for example.)

The final checkbox at bottom controls whether or not your computer requires a password when waking up from suspend. It's a good idea to keep this option checked – if you put your computer to sleep while logged into the system, this will keep an unauthorized user from gaining access to your data.

Generally, it's a good idea to set your computer to lock automatically, and to lock your computer when you leave it unattended for any reason. This will keep anyone else from messing with your computer or accessing your data.

LOGGING OUT OF THE COMPUTER

Logging out of a Linux Mint computer is quick and easy – in fact, it only takes three clicks of the mouse. To log out, first click on the mintMenu, and then click on the Log Out button in the left-hand column – it will look like a power button lying on its side:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_6d1a0cd9.jpg)

You will then see a dialog box asking whether or not you want to log out of the computer. Click Cancel if you've changed your mind and want to continue using the computer. Click Log out if you want to log out of the computer:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m78303484.jpg)

You will then log out, and the computer will return to the logon screen. Needless to say, it's a good idea make sure you have all your work saved first – some applications will warn you before you close with unsaved work, but not all will.

RESTARTING THE COMPUTER

Linux Mint is a remarkably stable operating system, and you can usually go for long periods of time without having to reboot your computer entirely. Nevertheless, you may have to reboot from time to time. You will almost always have to restart after installing updates, and certain applications might require you to restart. Additionally, if you install drivers for hardware devices (like a wireless card or a printer), you might have to restart, and if an application crashes in an odd way, that too might force you to restart.

To restart your Linux Mint system, go to the mintMenu, and click on the power button in the bottom of the left-hand column. You will then see a dialog box asking if you want to shut down or restart the computer. Click Cancel to if you've changed your mind and want to continue working. Click the Restart button if you want to restart your computer:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m1b094f9c.jpg)

Your computer will then restart. Needless to say, it's a good idea make sure you have all your work saved first – some applications will warn you before you close with unsaved work, but not all will.

SHUTTING DOWN THE COMPUTER

Finally, you will have to shut down your Linux Mint system from time to time. Hibernating the computer saves power, but if you need to save on power bills, nothing cuts electrical costs like shutting down the system entirely. And if you need to move a desktop computer, obviously you will need to shut it down completely.

Like logging out and restarting the computer, you can shut down your Linux Mint system through the system menu. Go to the mintMenu, and then click on the power button on the bottom of the left-hand column.You will then see a dialog box asking if you want to shut down or restart the computer. Click Cancel if you've changed your mind, but click the Shut Down button if you want to power off the computer:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m1b094f9c.jpg)

Your Linux Mint system will then power off. Needless to say, it's a good idea make sure you have all your work saved first – some applications will warn you before you close with unsaved work, but not all will.

UNDERSTANDING HOME FOLDERS

A “home folder” (also called a “home directory”) is simply the place where Linux Mint stores the files for individual users. The point of multiple user accounts on a computer is to keep everyone's documents separate, so it would defeat the point to let everyone store things in a big jumbled mess. You can actually see the home folders for all your accounts, if you go to the home folder in the top level of your computer's hard drive:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_d8b9ac3.jpg)

Within each home folder is a standardized set of folders:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m1f22e820.jpg)

Every user account in Linux Mint will come with the same set of folders – Documents, Pictures, Music, and so forth. (The contents of your Desktop are actually stored in the Desktop folder in your home folder.) By default, the applications in your Linux Mint system will make use of these folders. Web browsers will download files to the Download files, image-based applications will save pictures to the Pictures folder, LibreOffice will save documents to the Documents folder, and so forth.

However, if you produce a large number of documents and images, you'll quickly find your folders become unmanageable. A single folder in Linux Mint can hold thousands of files, but having to scroll through those files will become cumbersome. (Even searching with the Dash can become tricky with thousands of files in a single folder.) Fortunately, a folder can contain additional folders within it, commonly called “subfolders” or “subdirectories.” For example, you could create subfolders within your Documents folder to sort your documents by type – one for spreadsheets, and another for presentations – or any other organizational scheme you would prefer.

We'll show you how to create folders later in this chapter. First, we'll explain the application you actually use to navigate files and folders – the Nemo File Manager.

NEMO FILE MANAGER

Nemo is Linux Mint's built-in file management application – a program that displays your folders and the files within them in graphical format. To launch Nemo, simply click on the icon of the folder in the left-hand column of the mintMenu, or double-click on the home folder icon on your desktop.

The main window for Nemo usually looks like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m420b22d5.jpg)

Files and folders are displayed in the center of the window. To open a file or a folder, double-click on it. The list of links in the left-hand column is useful, since they will take you to the most common locations you will visit – your Documents folder, for instance.

You can use the left and right arrows to navigate forward and backward through folders you have visited. For instance, if you click on the Documents folder in your home folder, Nemo will take you to the Documents folder. To go back to your home folder, click on the back button (the arrow pointing to the left). Once you have returned to your home folder, Nemo can take you back to Documents by clicking on the Forward button (the arrow that points to the right). These two buttons work in much the same way as the Back and Forward buttons in a web browser.

The Nemo File Manager also offers a useful feature called “breadcrumbs”, which allows you to quickly backtrack out of folders. For example, let's say you are looking at a folder called MarchReports inside of another folder called Spreadsheets, which is in turn inside of your Documents folder. The breadcrumbs will then look like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_5e874772.jpg)

You can return to any of the folders by clicking on its name in the row of breadcrumbs. Clicking on Documents would return you to your Documents folder, while clicking any of the other breadcrumbs would take you to the folder identified in the breadcrumb.

Now that you know how to navigate through folders, we'll show you how to create one.

CREATING FOLDERS

Creating folders in Linux Mint is a simple process, and takes all of two mouse clicks.

To create a folder, first navigate to the location where you want to put the new folder. So if you want the new folder on your Desktop, you'd go to your Desktop. If you wanted to put the new folder in a different location, such as your Documents folder, go there instead.

Once you are at the desired location, right-click at an empty spot in the folder, and the context menu will appear:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_40f6911f.jpg)

From the context menu, select the Create New Folder option, which is at the top of the menu. You will then see a new folder, titled “untitled folder”, appear:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m7f3a9e5a.jpg)

The name of the folder (currently “untitled folder”) is in green, which means you can start typing a new name for the folder. Type a new name and hit enter, and Linux Mint will assign that name to the folder.

RENAMING FILES AND FOLDERS

You may need to change the name of a file or a folder for a variety of reasons. To rename a file or folder, right-click on the file or folder, and select Rename from the context menu:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m2c50155f.jpg)

The file or folder's name will then be highlighted in green. Type a new name, and hit Enter. The file will then be renamed.

COPYING AND MOVING FILES

Linux Mint and Nemo File Manager make copying and moving files a fairly simple procedure. There are a number of ways to copy files, and we'll go through them in this section.

First, navigate to the folder or file you want to copy. Right click on the folder or file to bring up the context menu, and then select Copy from the menu:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m2c50155f.jpg)

Next, navigate to the folder or drive where you want to copy the file or folder. Right click on a blank spot in the folder, and select Paste from the context menu:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_60476cd5.jpg)

Linux Mint will then make a copy of the file in the new location.

Suppose you want to move the file to a new location entirely, rather than copy it. You can do this as well, though it takes a few extra mouse clicks. First, right click on the file or folder, and select copy from the context menu:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m2c50155f.jpg)

After you have selected Copy, right-click on the file or folder again and select Cut from the context menu:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m2c50155f.jpg)

Then navigate in Nemo to the desired destination folder. Right-click on a blank spot in the folder, and click the Paste button:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_60476cd5.jpg)

Linux Mint will then “paste” the file in the new location. Copy, Cut, and Paste in Nemo works exactly like copying and pasting in a word processor or a spreadsheet application. The source file is deleted, and a copy of the file is created in the destination directory.

Additionally, you can also use what's called “drag-and-drop” to move files around from directory to directory. To do so, left-click on the file or folder you want to move, and hold down the left mouse button. The file will be highlighted. While continuing to hold down the left mouse button, drag the icon of the file to the new location. Linux Mint will then move the file to the new location.

(Note that if you drag-and-drop files from an external disk or to an external disk, Linux Mint only copies the files. For example, if you dragged-and-dropped a file from your USB flash drive to your Desktop, the file would be copied to your Desktop, but the original file would remain on the USB flash drive.)

What if you want to copy more than one file or folder at once? Like if you wanted to copy a hundred pictures from your digital camera's memory card to your Linux Mint system's Pictures folder? You could drag-and-drop or Copy and Paste each individual file, but this would be a massive waste of time. You could drag-and-drop the folder containing the picture files, but what if there are pictures mixed in the folder that you don't want to keep?

This is where SHIFT-clicking and CTRL-clicking come into play. Using SHIFT-clicking and CTRL-clicking, you can select multiple files simultaneously, and then copy or move them all at once. We'll look at SHIFT-clicking first.

SHIFT-clicking lets you select large quantities of files at once. To use it, first left-click on a single file:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m5a9ff76e.jpg)

Then hold down the shift key, and click on another file. You will notice that Linux Mint will then select every file between the first one you clicked and then file you clicked while holding down the SHIFT key:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m767a4184.jpg)

Using SHIFT-clicking, you can select a large mass of files or folders all at once. Then you can drag-and-drop them to a new destination, or right-click on them to Copy and Paste. But what if you only want to select six files scattered throughout a list of a hundred? SHIFT-clicking will move them all at once.

This is where CTRL-clicking will come in handy. Like SHIFT-clicking, CTRL-clicking allows you select multiple files simultaneously. But while SHIFT-clicking selects dozens or even hundreds of files and folders at once, with CTRL-clicking, you can select multiple files one by one, and then move, copy, or delete them.

First, left-click on the first file you want to move:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m5a9ff76e.jpg)

Then hold down the CTRL key and click on a second file:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_3d0aec48.jpg)

You'll notice that CTRL-clicking selects only the files you click on, and not all the files between them like SHIFT-clicking. CTRL-clicking lets you pick multiple files or folders and perform the same action on them simultaneously.

In the next section, we'll show you how to delete files.

DELETING FILES

In the old days of both Linux and Microsoft DOS, most personal computers did not have a graphical user interface, and so you had to delete files from the command line. And when you did, the files were gone forever – there was no easy way to get them back. Linux Mint, like many operating systems with a graphical user interface, makes things a little easier on the user with the Trash. The Trash is always in the left-hand navigation column of Nemo File Manager:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m501fc726.jpg)

The Trash is sort of a “holding pen” for deleted items. When you delete an item, instead of disappearing, it goes into the Trash. That way, if you delete something by mistake, it will sit in the Trash until you remember that you actually need it.

To move a file or a folder to the Trash, right-click on the file or folder in question. When the context menu appears, select Move to Trash from the menu:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_5c4eedc3.jpg)

The file or folder in question will then move to the Trash. Note that if you move a folder to the Trash, any files or subfolders the folder contains are also moved to the Trash, so take care when deleting folders.

What if you change your mind and want to bring a file back from the Trash? So long as you haven't emptied the Trash, you can bring files back. First, open the Trash by clicking on the Trash icon in the left-hand navigation column of Nemo File Manager.The interior of the Trash will look something like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m147aa37c.jpg)

You'll see all the files currently in your trash (assuming you haven't emptied it yet). To restore a file, click on it to select it (or SHIFT-click or CTRL-click to select multiple files at once), and then click on the Restore Selected Items button. The files and folders you selected will be returned to their previous locations on your computer.

One of the main reasons to delete files is to free up disk space, and so long as the files sit in your Trash, they will continue to take up disk space. To free up the disk space, and to permanently remove the files in the Trash, you have to empty the Trash. You can empty the Trash by clicking Empty Trash from within the Trash folder:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_2d9efcfa.jpg)

This will empty the Trash. Be careful using it – once you do, the files in the Trash will be gone forever.

***

## Chapter 3 - Creating Users and Groups

During the installation of Linux Mint, the installer prompts you to create an administrative account. If you're the only one to use your Linux Mint machine, that should be enough. But if you have more than one person using your Linux Mint system, you'll quickly need additional user accounts to keep everyone's files organized. Assigning permissions is well and good, but you need more than one user account to make permissions work properly. You may also find it necessary to organize those accounts into groups.

In this chapter we'll discuss how to create and delete users, and how to create and delete groups.

ADDING USERS

To start, let's discuss adding users to your Linux Mint system. You can do this through the GUI, quite easily. Merely go to the mintmenu, click on the Administration icon, and click on the Users and Groups item. This will bring up the Users and Groups utility.

From here, you can add and delete user accounts.

However, we've been focusing on how to do things from the command line, and you can add and remove users and groups quite easily with a few commands. For our example, let's say you want to add a user account for a woman named Caina Amalas to your Linux Mint system.

(Shameless authorial plug: Caina Amalas is the name of the character I've written for a series of ninteen sword & sorcery novels.)

To begin, it's best to choose some kind of naming convention for your user accounts. A naming convention sounds fancy, but it just means that you just stick to a consistent way of naming the accounts. Usually, something like the first initial and the last name is best - like "camalas" for Caina Amalas.

To actually create the new camalas user account, use the **useradd** command. You'll need root-level permission to create an account, so you'll have to use useradd with the sudo command:

**sudo useradd camalas**

However, this command by itself, without any options, is not very useful. It creates the camalas user account, but doesn't assign a display name for the account, nor does it create a home user for camalas. It also doesn't set any variables - for instance, if Caina logs in using the camalas account, she'll get the older sh shell for her command line, instead of the bash shell.

We'll need to add some options to the useradd command to make it more effective. To start, here's how to create a home directory with the command:

sudo useradd -m camalas

The -m option causes **useradd** to create a home directory. Next, we'll add another option, and tell useradd to set bash as camalas's default shell:

sudo useradd -m -s "/bin/bash" camalas

The addition of the -s switch and "/bin/bash" tells **useradd** to set the bash shell for camalas's default shell. Now we'll want to make sure that camalas's display name is properly set as Caina Amalas with the -c option:

sudo useradd -c "Caina Amalas" -m -s "/bin/bash" camalas

With these options, **useradd** creates a new account named camalas, sets the account's display name as Caina Amalas, creates a home directory for the new account, and sets bash for camalas's default shell. (Note that **useradd** has many options, and you can view them all in **useradd's** man page.)

There's one final thing you need to do to allow Caina to log in using the camalas account - you need to set a password for the new account. You can do that using the **passwd** command:

sudo passwd camalas

You can then set a password for camalas. Note that you can also use the **passwd** command, without sudo, to reset the password for your own account.

Linux Mint's user accounts are stored in the /etc/passwd file. It's a plain text file, so you can view it like any other text file:

cat /etc/passwd

You will see a lot of accounts in there, but most of them are for various system services and you needn't concern yourself with them. For actual user accounts, in /etc/passwd you can view the account name, the user id (UID) number, the group id (GUID) of the account's default group, the display name, the location of the home directory, and the default shell.

You might be tempted to manually add user accounts by editing the /etc/passwd file. Do *not* do this! The passwords for user accounts are stored in a restricted file called /etc/shadow, and it needs to stay in sync with /etc/passwd. Manually editing /etc/passwd can mess up your system.

REMOVING USER ACCOUNTS

From time to time, you'll want to remove accounts from your Linux Mint system. It's quick and easy to remove an account from the command line. In fact, it's rather less cumbersome than doing it through the GUI.

Before you delete a user account, you might first consider locking it with the **usermod** command. Locking an account disables its password, which means the account can no longer log into the system. For example, to lock the camalas account:

sudo usermod -L camalas

(Note that options, like commands and filenames, are case sensitive, and the -L option must be capitalized.)

If you want to get rid of an account entirely, use the **userdel** command with sudo:

sudo userdel camalas

This command will delete the camalas user account from your system. However, it will not delete camalas's home directory, which means that all her personal files and configuration settings will remain on your system in the /home/camalas folder. To delete both the camalas account and camalas's home folder, use **userdel** with the -r option:

sudo userdel -r camalas

This will delete both the camalas account and camalas's home folder.

ADDING GROUPS

Like user accounts, you can create groups for your users from the Linux Mint command line. There are a couple of different ways to create groups in Linux Mint, and both ways are valid. First, you can use the **groupadd** command to add a group named ghosts:

sudo groupadd ghosts

Alternatively, you could use the **addgroup** command:

**sudo addgroup ghosts**

Both commands do the same thing, but have different potential options, if you wish to peruse their man pages.

(Second shameless authorial plug: in the "Ghosts" novels, Caina belongs to the Ghosts, the spies of the Emperor of Nighmar.)

Like user accounts, Linux Mint stores all its groups in a plain text file, /etc/group. To view this file:

cat /etc/group

Most of the groups in there are system groups and can be safely ignored. It will seem like all of your user accounts are simultaneously listed in the group file as well - these are actually the primary groups of your user accounts (Linux Mint creates a group for each of your user accounts, and assigns the user account that group as its primary group). Any groups that you create will appear on the bottom of the file.

ADDING USERS TO GROUPS

Once you've created your group, you can add users to it. Again, there are a couple of different ways to do so. The first way is with the **useradd** command. To add the camalas account to the ghosts group:

sudo useradd camalas ghosts

You can also use the **usermod** command to add a user to a group:

sudo usermod -G ghosts -a camalas

REMOVING USERS FROM GROUPS

To remove an account from a group, use the **userdel** command:

sudo userdel camalas ghosts

This will remove camalas from the ghosts group.

DELETING GROUPS

To remove a group, use the **groupdel** command:

sudo groupdel ghosts

This will eliminate the ghosts group, even if it still has members.

Note that you cannot remove the primary group of any user without first either removing that user account from the group, or deleting the user account. (Remember that Linux Mint creates a group named after each of your user accounts.)

***

## Chapter 4 - An introduction to the command line

**WHAT IS THE COMMAND LINE?** 

The "command line" is shorthand way of saying the "command line interface", also commonly known as the "command prompt" or the "terminal." The command line is a text-based interface. Most people who have used a computer in the last twenty years are accustomed to a graphical interface, whether the various incarnations of Microsoft Windows or Mac OS. A graphical interface has windows, a mouse pointer, a scroll bar, icons, and other graphical representations of files and computer functions. A text-based interface, as the name suggests, has no graphics and relies entirely upon text. You type your commands into the command prompt, which usually looks something like this:

**jon@linuxmintmachine:~$**

Linux Mint then processes your commands and then returns with the results or, if you made a typographical mistake, an error message.

Why use the command line when Linux Mint comes with a highly functional GUI? For one thing, if you want to run Linux Mint as a server, you’ll need to know the command line, since a lot of server configuration can be done only via the command line. For another reason, many tasks are vastly more efficient from the command line.

Let’s say, for example, that you want to copy some JPEG files from your Pictures folder to an external hard drive called BACKUP. More specifically, let’s say you want to copy only those JPEG files that have the word “Jamie” in their name to the BACKUP drive. You could open up Pictures folder and drag every “Jamie” JPEG to the BACKUP drive one by one. Or you could open up a Terminal window and type this command:

**cp ~/Pictures/*Jamie*.jpg /media/BACKUP**

Hit Enter, and the command does all the work for you. No muss, no fuss.

CASE SENSITIVITY

Before we dig into the command line, we need to stress an important point.

*All commands and filenames in Linux are case-sensitive!*

This can really confuse people coming over from a Windows/DOS background, since neither the old DOS operating system nor the Windows command line were case-sensitive. In other words, Windows would view the files Book.doc, book.doc, and BOOK.doc as the same file. Linux, however, will recognize those as three different files.

In the same way, Linux commands are case sensitive. In Windows/DOS, typing dir, Dir, and DIR into the command prompt will trigger the same **dir** command, which gives a listening of files in the current directory. Linux commands are case-sensitive – ls, Ls, and LS are not the same thing.

Bear this in mind while using the command line.

FILENAMES WITH SPACES

The command line does not handle spaces well - say you tried to use the following command to delete a file named "Bob's Term Paper."

**rm Bob's Term Paper**

This command would fail because the command line would interpret each word in the command as a separate file. To force the command line to view the file properly, enclose any filename with spaces within quotation marks:

**rm "Bob's Term Paper"**

This time rm will delete the file.

HOW TO ACCESS THE COMMAND LINE

If you’ve never used the command line in Linux Mint before, you might not know how to access it. Fortunately, it’s quite simple. There are two ways to launch the command line.

The first way is to go to the the mintMenu, and then to click on the Terminal icon in the left-hand column. This will launch the GNOME Terminal emulator application, which lets you launch commands from within the GUI.

The second way is to hit the CTRL-ALT-F1 keys on your keyboard. Do this, and the GUI will disappear, replaced by a black screen with a logon prompt in white text. Don’t be alarmed! This is a “virtual console”, which lets you shift the GUI to the background and log in again in a command-line only mode. Your logon session with the GUI will be unaffected – Linux Mint allows multiple logons from the same user at the same time.

You can return to the GUI at any time by hitting CTRL-ALT-F7.

Note that Linux Mint allows you to have seven virtual consoles, from F1 to F7\. F7 is reserved for the GUI, and the remaining six allow you to log on using the command line.

THE COMMAND PROMPT ITSELF

The command prompt itself, as we’ve mentioned, will probably look something like this:

**jon@linuxmintmachine:~$**

But what does that mean? Let’s break it down.

The “jon”, the part before the @ symbol, is the name of the user currently logged into the system. If I am logged into my Linux Mint machine as “jon”, then that’s the username I’ll see before the @ symbol.

The “linuxmintmachine”, the part after the @ symbol, is the hostname, or the name of the computer. So if my Linux Mint machine is named “linuxmintmachine”, then that’s the hostname you’ll see in the command prompt.

The colon (:) marks the division between the part of the prompt that identifies the user and the machine - jon@linuxmintmachine - and the part of the prompt that displays the current working directory, which we'll explain below.

The ~ mark refers to the current working directory – in other words, the folder you are currently occupying. (The terms "directory" and "folder" are used interchangeably, though "directory" is used more often in the context of the command line.) In Linux and UNIX, the tilde symbol “~” is shorthand for the user’s home directory. So, if I am logged into linuxmintmachine as jon, then the ~ is shorthand for the **/home/jon** directory.

This means that if you change your working directory, the command prompt changes as well. Let us say that you change your working directory to /, which in Linux is the root directory. The command prompt will then look like this:

**jon@linuxmintmachine:/$**

Or if you change the working directory to /etc/hp, the prompt will look like this:

**jon@linuxmintmachine:/etc/hp$**

Let’s take a look at some useful basic commands.

FINDING THE WORKING DIRECTORY

The “working directory” refers to the directory where the command prompt is currently focused. As we mention above, the working directory is shown in the command prompt. However, some Linux configurations do not include the working directory in the command prompt by default. To find the working directory, use this command:

**pwd**

If you’re in your Documents folder (a subfolder of your home directory), the output will look something like this:

**/home/jon/Documents**

Next, let’s discuss moving about the Linux Mint filesystem.

MOVING FROM DIRECTORY TO DIRECTORY

You can use the cd command to move from directory to directory from the command line. If you wanted to go to your home directory, for example:

**cd ~**

To change to the root directory:

**cd /**

To fully utilize the cd command (and some of the other commands discussed below) you’ll need to understand the concept of file paths in Linux Mint.

A “file path” refers to a file’s location within the filesystem. Let’s say you have a document file named Book.doc stored in your Documents folder. So its absolute location, its exact place in the filesystem, would be this:

**/home/jon/Docments/Book.doc**

So if you wanted to move to /home/jon/Documents from anywhere in the filesystem, you would use this command:

**cd /home/jon/Documents** 

However, you don’t need to type the full path for directories that are subdirectories of the current working directory. If you’re already in your home directory, you don’t need to type the full path to change to Documents, since Documents is a subdirectory of your home directory. Simply type this:

**cd Documents**

You can use a similar shortcut to return to the previous directory:

**cd ..**

The cd command followed by a space and two periods will return you to the next directory up, from Documents to your home folder. Nor does this work only in your home folder – you can use **cd ..** anywhere in the filesystem, and it will move you to your current directory’s parent directory.

Of course, once you’re inside the directories, you’ll actually want to view their contents.

LISTING THE CONTENTS OF DIRECTORIES

To view the contents of a directory, use the ls command:

**ls**

If you use **ls** in your home directory, the output will probably look something like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m14f57c9.jpg)

By default, **ls** lists the contents of the current working directory. If you want to view the contents of a different directory, you can either navigate there via the **cd** command, or type the absolute path with the **ls** command. For instance, to view the full contents of the /etc directory:

**ls /etc**

Pretty simple, right? But the **ls** command doesn't offer very much information. This is a good place to bring up the idea of command options, also known as command switches.

In the context of Linux commands, an “option” is a modifier to a command. It tells the command to perform a slightly different function, or to alter the output somewhat. Run the **ls –l** command in your home directory, and look at how the output changes:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m2e751004.jpg)

The “l” option stands for “long listing”, and ls then shows much more information it does without the option, including the permissions and ownership of the file, along with the file’s size and timestamp.

The **ls -l** command is even more useful when combined with the -h option:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_1fe36ac2.jpg)

You can see how the size of the files are now listened in kilobytes and megabytes, which is often easier to read than just bytes.

You can also use the **ls** command with the -a switch to view hidden files:

ls –a

Note all the hidden files in your home directory:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m26bc43a9.jpg)

(Most of these hidden files are configuration settings for your account, and should be left alone unless you have a good reason to alter them.)

In Linux, files are hidden by placing a “.” in front of their name. You can hide files yourself by using the **mv** command, which we’ll discuss in the next section.

MOVING AND RENAMING FILES

To rename a file, you can use the **mv** command. Let’s say you wanted to rename the Book.doc file in the current working directory to Roughdraft.doc:

**mv Book.doc Roughdraft.doc**

The **mv** command will then rename the Book.doc file to Roughdraft.doc.

The mv command can also (as the name suggests) move files from one location to another on your system. If you wanted to move Book.doc from your Documents folder to another folder called Backup in your home directory, you would use the **mv** command like this:

**mv ~/Documents/Book.doc ~/Backup**

The mv command also works with “wildcards”, which are characters that can represent file names. Think of them as variables – you can use them to tell the **mv** command to move “every file that ends with .doc in my Documents folder to the Backup folder.” It works like this:

**mv ~/Documents/*.doc ~/Backup**

This will move every single file with the .doc extension in your Documents folder to your Backup folder.

CREATING DIRECTORIES

The **mkdir** command lets you create directories. To create a directory named NewDirectory in the current working directory:

**mkdir NewDirectory**

You can also create directories by absolute path. To create a directory named NewDirectory in your Documents folder:

**mkdir ~/Documents/NewDirectory**

DELETING FILES AND FOLDERS

Sooner or later, you'll need to delete some files or folders, and the **rm** command will let you get rid of them. To get rid of a file named Book.doc in the current working directory:

**rm Book.doc**

You can also use **rm** to delete files by their absolute path:

**rm /home/jon/Documents/Book.doc**

Wildcards also work with **rm**. You can use **rm** to, say, delete every single .doc file on your Documents folder:

**rm /home/jon/Documents/*.doc**

Needless to say, you will want to be extremely careful when using wildcards with **rm**! If you make an error, you can unintentionally wipe out a large chunk of your files.

You can also remove directories from the command line. To remove an empty directory, use the **rmdir** command:

**rmdir NewDirectory**

However, note that **rmdir** will only work if the target directory is empty. If it's not, you'll have to clean out any files in the directory before you can delete it with **rmdir**.

Alternatively, you can use the **rm** command with the recursive -r option to delete a directory, all its files, and any subdirectories (along with their files):

**rm -r NewDirectory**

You'll want to be especially careful when using the rm command with the -r option! You can easily wipe out entire branches of the filesystem, and can lose important data if you're not careful.

COMPRESSING AND UNCOMPRESSING FILES

Modern hard drives are enormous - as of this writing it's common for laptops to have hard drives of three hundred and twenty gigabytes or more, while desktop machines can have hard drives upwards of a terabyte. So compressing files might not seem like such a big deal. However, compressing files is still useful for creating backups, and many files that you download off the Internet will come in compressed form. When working in the command line environment, you'll need to know how to uncompress these files.

Linux Mint uses the **tar** command to create file "archives", which are a large number of small files combined into one large file for easy storage and copying. The **tar** command dates back to the earliest days of UNIX, and is very efficient. For example, let's say you wanted to create a file named "backup.tar" containing all the files and folders in your Documents folder. You would use the **tar** command with the -c option to create an archive, and the -f option to specify a name for the archive:

**tar -cf backup.tar ~/Documents**

In short order, **tar** will create the "backup.tar" file. Remember when using the **tar** command to always add the *.tar extension to any filenames, since **tar** will not do so automatically.

However, this new archive isn't compressed at all. It takes up the same amount of space as your ~/Documents folder. To compress it, you'll need to use **tar** with the -z switch, which compresses the archive with gzip compression:

**tar -czf backup.tar.gz ~/Documents** 

You might also want to add the -v option to the command, as well:

**tar -czvf backup.tar.gz ~/Documents** 

The -v command tells **tar** to produce verbose output, which means it tells you exactly what it is doing, and informs you if someting goes wrong.

To unpack files from a **tar** archive, you likewise use the **tar** command, but with the -x switch to *eXtract* the files, rather than the -c switch to *Compress* them:

**tar -xvf backup.tar** 

If a **tar** archive has been compressed with gzip style compression, make sure to add the -z command option to the mix:

**tar -xzvf backup.tar.gz** 

The **tar** command is useful, but complicated. It's somewhat easier to use the **zip** and **unzip** commands. To compress your Documents folder with **zip** into an compressed archive named "backup.zip", use the **zip** command with these options:

**zip -r backup.zip ~/Documents**

Uncompressing the archive merely takes the **unzip** command:

**unzip backup.zip** 

Note that the files are uncompressed in the same directory as the backup.zip file.

VIEWING FILES

Moving files, compressing files, and deleting files is useful, but sometimes you'll need to view them as well. A great many files in Linux Mint, especially configuration files, are simply text files, and you can view them with the **cat** command. To view a file named document.txt in the working directory:

**cat document.txt** 

Very often a text document will be too long to fit on a single screen, and will scroll up before you can view the entire thing. You can pipe the output of the **cat** command to the **more** command, which will let you view the file one screen at a time:

**cat document.txt | more** 

"Pipes" in Linux allow you to direct the output of one command to another command, which then acts upon that output.

The **less** command essentially combines the **cat** and the **more** commands, letting you scroll through the text file:

less document.txt

Sometimes you'll just want to view the first few lines of a file. You can do so with the **head** command:

**head** **document.txt**

This will display the first five lines of the file. Alternately, you can use the **tail** command to view the final five lines of a file:

**tail document.txt**

Sometimes you'll want to sort through a document for a particular term, which can take some time. The **grep** command, which searches output, can find a particular search string within the output. Pipe the output from the **cat** command to **grep**, and it will find any instances of that term:

**cat document.txt | grep term**

USING ROOT POWERS

As you do things on Linux Mint, you'll quickly notice that a great many areas of the system are restricted. You cannot, for instance, go to the /bin directory and start deleting files at random. This is a good thing - it prevents you from accidentally doing damage to your system (or malicious users from doing damage on purpose).

However, there are times when you'll need to install a program, or edit a configuration file, or perform some other administrative task. To do that, you'll need root-level permissions. The "root" account, also called the superuser account, is the most powerful user on a Linux system. The root account can delete any file and change any setting. For security reasons, the root account is disabled by default on Linux Mint systems, since it presents a tempting target to attackers.

To get around this, Linux Mint uses the **sudo** command, which allows a user to temporarily act as root. To use a command with **sudo**, simply preface it with the **sudo** command:

**sudo rm document.txt**

The command will ask for your password, and after you enter it, **rm** will run with root-level access.

(Note that only administrative users on a Linux Mint system can use root. By default, the account you create during installation is an administrative user.)

BASIC CALCULATOR

Linux Mint also comes with a handy little utility called the **bc** command – the “bc” stands for “basic calculator”. The **bc** command lets you perform quick, simple mathematical operations from the command line, which can be easier than reaching for your desktop calculator or firing up a graphical calculator (and if you’re using the server version of Linux Mint, no GUI calculator is available, obviously).

To use **bc**, first type this command:

bc

This will take you to the **bc** prompt, and you can now perform mathematical operations. To add two numbers, for instance, type this, and then hit the Enter key:

2 +2

To subtract two numbers, use this syntax:

2 -2

To divide two numbers, use the / key:

2 /2

For multiplication, use the * key:

2 * 2

Use fractions instead of decimals:

2.5 + 1

Once you are finished with bc, type quit to return to the normal command prompt:

quit

BASH SHELL TIPS

For its command-line interface, Linux Mint uses a program called the bash shell. The term "shell" refers to a program that provides an interface between the user and the operating system. The bash shell is a descendant of the old Bourne sh shell - the name "bash" itself is a pun meaning "Bourne-again shell." There are a number of other shells available, but most people agree that bash is the best one available (opinions can, of course, differ). And bash has a number of useful features.

The first is what's called "command/filename completion." What that means if that you type a partial command or filename, and hit the TAB key, bash will take a good guess at completing the filename or command. Say you have a file named ReallyReallyReallyLongLongLongFileName.txt, and you want to delete it. But you don't want to type out that entire filename. Instead you can just start to type it:

rm ReallyR

And then hit the tab key. The bash shell will finish out the file name for you:

rm R ReallyReallyReallyLongLongLongFileName.txt

The bash shell also has a neat feature called command history. If you hit the Up arrow key on your keyboard, you can scroll back through the history of commands you have used. If you can't remember a long command you just used, or you don't want to retype, this can come in handy.

The bash shell stores your command history in a file named .bash_history in your home folder. To view it, use this command:

cat ~/.bash_history

Note that this file only gets updated when you log out of the system.

GETTING HELP

There's no getting around it - Linux commands are complicated, and come with a vast array of options and options, and all of that is difficult to remember. Thankfully, Linux Mint comes with a built-in help system - the **man** command. Short for "manual", **man** lets you view the basic usage and options for the command. To use it, simply type **man** and the name of the command whose manual page you want to read:

**man ls**

This will bring up the manual page for the ls command. You can use the page up and page down keys to navigate through the man page, and once you're finished, pressing the "q" key will return you to the command prompt.

***

## Chapter 5 - Checking Memory and Disk Space Usage

When it comes to dealing with computers (whether Linux Mint, Windows, or Mac OS X systems), there is one infallible rule - there's never enough memory or disk space. Granted, the situation has gotten better than the old days of DOS, when you had only 640 kilobytes of memory to use. Personal computers have gotten more powerful, and as of this writing you can buy a laptop computer with four gigabytes of memory and a five hundred gigabyte hard drive for about $300 to $400 USD (even less if the computer is a desktop). So for the average user, carefully managing your personal computer's memory and disk space isn't quite as critical as it once was.

However, you'll still want to keep an eye on memory and disk usage. If your Linux Mint system slows down, you'll want to know why, and examining resource usage can give you a clue as to the cause. If your hard drive fills up, you'll want to find which files are taking the most room. And if you are managing a Linux Mint server system with multiple users accessing it simultaneously, you will definitely want to keep a close eye on resource usage, lest one user bring the server to a crashing halt.

In this chapter we'll look at how to monitor Linux Mint's usage of system resources, both with graphical and command line tools.

SYSTEM MONITOR

System Monitor is a utility that provides a wealth of real-time information about the status of your system. From System Monitor, you can see how much RAM and hard drive space your system has free. You can also view graphs charting CPU usage, the amount of memory used by the various processes running on your system, and the amount of free space on any additional disks (like flash drives or external hard drives) attached to your computer.

To launch System Monitor, click on the mintmenu and search for it in the search field. Click on the program's icon, and System Manager should launch in short order.

System Monitor has three tabs, each presenting different information, that we’ll look at from left to right.

“Processes” is the first tab. A “process” is the technical term for any program running on your system, whether a background daemon (a program that provides services), or any programs that you or any other users launch. The Processes tab has a number of columns that provide useful information. The first column, “Process Name”, provides the name of the process. The “% CPU” tab shows the amount of the CPU’s processing time the process is consuming. The “ID” column shows the process’s ID number, which comes in handy if you need to force it to end from the command line (which we will describe in Chapter 22). The “Memory” column shows the amount of memory the process is using. Finally, the Processes tab has an End Process button in the lower-right hand corner, which you can use to forcibly shut down unresponsive processes.

The second tab, “Resources”, provides three real-time graphs. The first graph, “CPU History”, shows the amount of CPU time being consumed. If you have a multi-core processor (as most computers do nowadays), the graph will represent the different CPU cores with different colors. The second graph, “Memory and Swap History”, shows the amount of RAM and swap file space being used. (“Swap file” refers to virtual memory, a partition on your hard drive that Linux Mint uses as temporary RAM if the real RAM fills up.) The final graph, “Network History”, shows the amount of incoming and outgoing traffic to your system’s network adapter.

The final tab “File Systems” shows any file systems – that is, disks – attached to your Linux Mint system. This includes hard drives, optical disks (like CDs and DVDs), USB external hard drives, and USB flash drivers. The columns show the actual device names for the drives (usually something like /dev/sda1), the mount point (where the device is mounted in the filesystem), the type of filesystem, and the amount of space on the device, both total space and free space.

System Monitor offers a lot of useful information in one convenient place, but it’s a graphical application, which means that it doesn’t work from the command line. To check this information from the command line, you’ll need to use the top command, which we’ll discuss in the next section.

THE TOP COMMAND

The top command has been around forever, and is included in practically every variant of Linux. Linux Mint is no exception. The top command displays a variety of useful statistics, including the “top” users of CPU time (hence the command’s name). To launch top, simply type the command at the command prompt:

top

Once launched, top stays running, displaying statistics in real time. Processes are listed by their process ID number, along the name of the command that started the process. There’s a lot of information listed in top, so let’s take a look at the available statistics:

PID: A process’s process ID number.

USER: The process’s owner. Processes owned by root are usually system processes, and should be left alone unless they cause problems.

PR: The process’s priority, which determines how much attention the CPU will give this process over other processes. The lower the number, the higher the priority.

NI: The nice value of the process, which affects its priority.

VIRT: How much virtual memory the process is using.

RES: How much physical RAM the process is using, measured in kilobytes.

SHR: How much shared memory the process is using.

S: The current status of the process (zombied, sleeping, running, uninterruptedly sleeping, or traced).

%CPU: The percentage of the processor time used by the process.

%MEM: The percentage of physical RAM used by the process.

TIME+: How much processor time the process has used.

COMMAND: The name of the command that started the process.

Of course, you may want to sort the top display by a certain category from least to greatest. This is especially useful when you want to figure out what process is hogging the most CPU time or memory. Hitting the ‘t’ key will sort the processes by CPU time. Hitting ‘l‘ will sort by load average, and ‘m‘ by memory info.

Like System Monitor, you can also use top to kill uncooperative processes. To do this, you’ll need to make note of the process ID you want to kill. Hit the “k” key while top is running, and the utility will ask you to input a process ID number. Input the number, hit Enter, and then hit Enter again when it asks if you want to kill the process (top assumes you mean “yes” when you hit enter). The top utility will then kill the process.

Once you’ve finished with top, hit the q key to exit and return to the command line.

CHECK DISK SPACE USAGE

The top command can do quite a lot, but there’s one thing that System Monitor can do that top can’t – it can show the amount of used disk space. And keeping track of the used space on your hard drive is important. Granted, these days computers come with enormous hard drives - a capacity of one or even two terabytes in a desktop machine is quite common. Of course, the size of popular files has only gotten larger (video takes up an enormous amount of space), making it all the easier to fill up your hard drive. And filling up your hard drive can cause all sorts of unintended problems, especially on a server system.

Fortunately, there are several commands you can use to track disk space usage from the command line in Linux Mint.

The first command is **df**, which produces an output like this:

/dev/sda1 31621016 3364900 26649820 12% /

You'll notice like the Filesystems tab in System Monitor, the df command lists all the filesystems on your computer. The first number is the total size of the drive. The second is the used space. The third is the available space, and the final number is the percentage of space used. However, the numbers are in 1 kilobyte blocks, which makes the difficult to read without mental mathematics. To make the output more readable, use **df** with the -h option:

/dev/sda1 31G 3.3G 26G 12% /

You'll notice that the sizes are now in gigabytes (or megabytes, depending on the size of the filesystem), which is much more readable.

You might also need to check the size of an individual folder, since the ls command, even with the -l option doesn't bother to list the size of folders. (Technically, directories in Linux are also files, so the **ls -l** command only lists the size of the file representing the directory without any of the directory's contents.) To find the size of a folder from the commmand line, use the **du** command with the -s and -h options:

du -sh ~

The command will list the size of the targeted folder in megabytes or gigabytes, as appropriate.

CHECK MEMORY USAGE

The top command does a pretty good job of seeing which processes are using the most memory. It does not, however, give an overview of your system's entire memory. To do so, you need to use the **free** command, which generates an output like this:

Mem: 1025700 340708 684992 0 38904 156368

The first three numbers are the most important - they list the total amount of RAM, the amount used, and the amount currently free. The RAM is listed in bytes which, unless you're really good at mental math, makes it rather hard to read. Fortunately, you can use the -m option with **free** to display the totals in megabytes instead of bytes, generating an output like this:

Mem: 1001 501 500 0 64 277

The numbers are roughly the same as before, but they're expressed in megabytes now, not bytes, which usually makes for easier reading. You can also use the -k and -g switches to express the values in kilobytes and megabytes, if you prefer.

***

## Chapter 6 - Installing Software

For people used to the Microsoft Windows system, it can be to difficult to figure out how to install software on a Linux Mint system. Usually, on a Windows machine, you download the installer file from the website, double-click on it, and follow the steps suggested by the install wizard. Or you insert the CD or DVD into your optical drive and follow the AutoPlay prompt, or navigate to the DVD's root menu through Windows Explorer and double-click on the SETUP.EXE file. One of the strengths of the Microsoft Windows is the relative ease of installing software on a Windows computer, and the enormous library of software available for Windows. (In fact, the ease of installing software on Windows can be a weakness - consider how easy it is to catch malware on a Windows box.) Unfortunately, this vast library of software (usually) will not work on Linux Mint. (Unless you have Wine, which we'll discuss in Chapter 15.)

Fortunately, Linux Mint is a Linux distribution. While it may not have access to the Windows software ecosystem, it nonetheless has access to the vast library of Linux applications and utilities. And as an added bonus, many of these applications are free - both free to use and free to alter and distribute without legal encumbrance.

There are four basic ways to install software programs on your Linux Mint system: the Software Manager, Synaptic Package Manager, .deb installer files, and the command line. All of them are fairly easy to use. Server-level applications usually take some more work, but installing end-user applications is straightforward. Our focus in this book is on the command line, but we'll also go through the graphical ways of installing applications.

Note that you'll need an admin account on your Linux Mint system to install software - the default account you create during installation counts as an admin account.

REPOSITORIES

However, before we start, you'll need to understand the concept of a software repository. Basically, a software repository is a server on the Internet where the installer packages for software programs are stored. ("Packages" are software installers that are pre-compiled to work with a particular operating system, usually specific versions of Linux.) Client computers can then access those repositories, download the packages, and install the programs. This more efficient than, say, distributing software via CD or DVD, or by downloading the installer from a web server.

Canonical operates a number of software repositories, divided into roughly four groups. The "main" repository holds open source software maintained by Canonical. The "universe" repository contains open source software from other groups. The "restricted" repository holds non-free software necessary for device drivers (there is a lack of free Linux drivers for video cards and wireless network adapters, in particular). Finally, the "multiverse" repository contains non-free software restricted by either copyright or legal issues, or both.

It's possible to add additional repositories to your system - we'll discuss how to do that shortly.

SOFTWARE MANAGER

To launch Software Center, go to the mintMenu, to the Administration category, and click on the icon for Software Manager. Enter your password to authenticate (note that you must be an administrative user to use Software Manager), and Mint will launch Software Manager for you.

You can search for applications to install, both through the entire catalog and within specific categories, by using the search box in the upper right-hand corner of the window. You can search for applications either by specific name, or by terms in their descriptions.

Installing applications is a breeze; merely double-click the application you want, and click the Install button. After you enter your password to authenticate, Software Manager will link up with the repositories, and download and install the application you want.

Software Manager is far and away the easiest way to install software on Linux Mint - but it doesn't work from the command line.

SYNAPTIC PACKAGE MANAGER

The second way to install software through the GUI is using the Synaptic Package Manager. Synaptic is essentially a graphical interface to apt, the Advanced Packaging Tool, which is a utility that handles the installation of software on Debian Linux and Debian-derived distributions (such as Linux Mint). You can launch Synaptic by clicking on the mintMenu, going to the Administration category, and clicking on the icon for Synaptic. Synaptic needs root powers to run, so you'll need to enter your password to confirm. After you do, Synaptic will open.

Synaptic's graphical interface isn't quite as friendly as Software Manager's, and can be confusing to use. Synaptic's big advantage is that it lists every single package available in any software repositories you have configured your system to use. Even better, the list is searchable - if you don't know the name of a package, you can search for it by name or description. For example, if you wanted to install Virtualbox, but didn't know the name of the package, you could search for any packages with "Virtualbox" in their name, and find what you need in short order.

Synaptic will also let you upgrade all the installed programs on your system at once, assuming that upgrades are in fact available in the software repositories. The "Mark All Upgrades" button will search out any upgrades, and mark the packages that can be upgraded. You can then hit the Apply button to download and install the upgrade packages.

DEB PACKAGES

The Linux Mint software repositories store a vast selection of software, but they do not contain every last available application for Linux Mint. Sometimes developers prefer not to keep their software in the repositories for a variety of reasons, or prefer to make the application available themselves. Very often the installer for such a program will be distributed in what's called a deb file. The developer will make the deb file available for download on their website. (As of this writing, Google keeps most of its applications - Chrome, Picasa, and the like - available as deb files on the download section of the Google site.)

To install an application from a deb file, simply download it and double-click it to run. (Ironically, despite the differences we discussed earlier, this is almost like installing software for Windows.) Depending on how the deb file is put together, you'll either be redirected to the Linux Mint Software Center, or presented with a the graphical front end for the dpkg tool (the application that installs deb packages - we'll discuss it more in the next section). In either case, you'll hit the Install button, enter your password to confirm, and the application will install itself on your system.

INSTALLING SOFTWARE FROM THE COMMAND LINE

Synaptic itself is only a graphical interface for the Advanced Packaging Tool, or "apt", as it is more commonly known. The apt tool, as we mentioned above, automates the installation of software on Debian and Debian-derived systems (like Linux Mint) by downloading the package files from the repository and installing them. You can use apt to install, upgrade, and remove software from the command line, and apt makes the process quick, easy, and painless.

(Note that you CANNOT use apt while Synaptic is also open, since both Synaptic and apt need to lock the /var/lib/dpkg/lock directory while installing software. This is a common mistake - people will look up a package's name in Synaptic, and then go to the Terminal to install it, forgetting to close Synaptic first.)

To use apt, you need admin rights to your system, as well as the name of the package you want to install. Let's say that you want to install the AbiWord processor application on your computer. The name of AbiWord's installer package is simply "abiword", and it's in the Linux Mint repositories. To install it, you'd simply use this command:

sudo apt-get install abiword

(Installing software almost always must be done as root.)

Enter your password to authenticate, and apt-get will download AbiWord from the repositories and install it for you. If you change your mind, apt also makes it easy to remove software:

sudo apt-get remove abiword

(Again, you need root permissions to remove software, along with the name of the application.)

Like Synaptic, apt can also upgrade any packages on your system that have upgrades available in the repositories. First, use apt-get to update your system's listing of its repositories:

sudo apt-get update

This usually takes a few minutes to run. After the command finishes, you can then upgrade any packages with upgrades available:

sudo apt-get upgrade

This command might take a while, depending on how many upgrades are available (and how large the upgrades are). But after it's done, the software on your system will be up to date.

Finally, you can also install deb packages from the command line, which is a necessity if you want to install a deb package in the Server edition of Linux Mint. To install a deb file called installer.deb:

sudo dpkg -i installer.deb

Likewise, **dpkg** can also remove software with the -r option:

sudo dpkg -r installer.deb

INSTALL SOFTWARE FROM A PERSONAL PACKAGE ARCHIVE

Some developers take a halfway point between putting their application in the Linux Mint repositories or distributing as a deb file. They instead create a "personal package archive", commonly abbreviated as a PPA, to house their application's installer. Users can then connect to the PPA and use apt to download and install the application. Very often this happens with new applications that haven't yet been included in the Linux Mint repositories, or applications that are still in beta or even the alpha testing stages.

(Before going any further, we should emphasize that you should install software from a PPA only if the developer is reputable - an unscrupulous software developer could create a fake PPA with installers for malicious software.)

For example, say you want to install an application called "viewer". It's not available in the Linux Mint repositories, but the developer maintains a PPA called "viewer/viewer-releases". Here's how you would add the PPA to your Linux Mint system:

sudo add-apt-repository ppa:viewer/viewer-releases

Then update your system's listing of the repositories, to force it to index the new PPA:

sudo apt-get update

After that command is finished, you are now free to download and install the viewer application:

sudo apt-get install viewer

***

## Chapter 7 - Checking Memory and Disk Space Usage

When it comes to dealing with computers (whether Linux Mint, Windows, or Mac OS X systems), there is one infallible rule - there's never enough memory or disk space. Granted, the situation has gotten better than the old days of DOS, when you had only 640 kilobytes of memory to use. Personal computers have gotten more powerful, and as of this writing you can buy a laptop computer with four gigabytes of memory and a three hundred and twenty gigabyte hard drive for about $500 (even less if the computer is a desktop). So for the average user, carefully managing your personal computer's memory and disk space isn't quite as critical as it once was.

However, you'll still want to keep an eye on memory and disk usage. If your Linux Mint system slows down, you'll want to know why, and examining resource usage can give you a clue as to the cause. If your hard drive fills up, you'll want to find which files are taking the most room. And if you are managing a Linux Mint Server system with multiple users accessing it simultaneously, you will definitely want to keep a close eye on resource usage, lest one user bring the server to a crashing halt.

In this chapter we'll look at how to monitor Linux Mint's usage of system resources, both with graphical and command line tools.

SYSTEM MONITOR

System Monitor is a utility that provides a wealth of real-time information about the status of your system. From System Monitor, you can see how much RAM and hard drive space your system has free. You can also view graphs charting CPU usage, the amount of memory used by the various processes running on your system, and the amount of free space on any additional disks (like flash drives or external hard drives) attached to your computer.

To launch System Monitor, click on the Dash and search for it in the search field. Click on the program's icon, and System Manager should launch in short order.

System Monitor has four tabs, each presenting different information, that we’ll look at from left to right.

“System” is the first tab, and as the name suggests, it presents basic information about your system. At the top you’ll see your system’s hostname, followed your system’s version of Linux Mint and version of the Linux kernel. You’ll also see the total amount of RAM your system has installed, along with the type and speed of your CPU. Below that, you’ll see the available disk space on your hard drive (if you have multiple hard drives installed, it will show the free space on the drive that has your Linux Mint installation).

“Processes” is the next tab. A “process” is the technical term for any program running on your system, whether a background daemon (a program that provides services), or any programs that you or any other users launch. The Processes tab has a number of columns that provide useful information. The first column, “Process Name”, provides the name of the process. The “% CPU” tab shows the amount of the CPU’s processing time the process is consuming. The “ID” column shows the process’s ID number, which comes in handy if you need to force it to end from the command line. The “Memory” column shows the amount of memory the process is using. Finally, the Processes tab has an End Process button in the lower-right hand corner, which you can use to forcibly shut down unresponsive processes.

The third tab, “Resources”, provides three real-time graphs. The first graph, “CPU History”, shows the amount of CPU time being consumed. If you have a multi-core processor (as most computers do nowadays), the graph will represent the different CPU cores with different colors. The second graph, “Memory and Swap History”, shows the amount of RAM and swap file space being used. (“Swap file” refers to virtual memory, a partition on your hard drive that Linux Mint uses as temporary RAM if the real RAM fills up.) The final graph, “Network History”, shows the amount of incoming and outgoing traffic to your system’s network adapter.

The final tab “File Systems” shows any file systems – that is, disks – attached to your Linux Mint system. This includes hard drives, optical disks (like CDs and DVDs), USB external hard drives, and USB flash drivers. The columns show the actual device names for the drives (usually something like /dev/sda1), the mount point (where the device is mounted in the filesystem), the type of filesystem, and the amount of space on the device, both total space and free space.

System Monitor offers a lot of useful information in one convenient place, but it’s a graphical application, which means that it doesn’t work from the command line. To check this information from the command line, you’ll need to use the top command, which we’ll discuss in the next section.

THE TOP COMMAND

The top command has been around forever, and is included in practically every variant of Linux. Linux Mint is no exception. The top command displays a variety of useful statistics, including the “top” users of CPU time (hence the command’s name). To launch top, simply type the command at the command prompt:

top

Once launched, top stays running, displaying statistics in real time. Processes are listed by their process ID number, along the name of the command that started the process. There’s a lot of information listed in top, so let’s take a look at the available statistics:

PID: A process’s process ID number.

USER: The process’s owner. Processes owned by root are usually system processes, and should be left alone unless they cause problems.

PR: The process’s priority, which determines how much attention the CPU will give this process over other processes. The lower the number, the higher the priority.

NI: The nice value of the process, which affects its priority.

VIRT: How much virtual memory the process is using.

RES: How much physical RAM the process is using, measured in kilobytes.

SHR: How much shared memory the process is using.

S: The current status of the process (zombied, sleeping, running, uninterruptedly sleeping, or traced).

%CPU: The percentage of the processor time used by the process.

%MEM: The percentage of physical RAM used by the process.

TIME+: How much processor time the process has used.

COMMAND: The name of the command that started the process.

Of course, you may want to sort the top display by a certain category from least to greatest. This is especially useful when you want to figure out what process is hogging the most CPU time or memory. Hitting the ‘t’ key will sort the processes by CPU time. Hitting ‘l‘ will sort by load average, and ‘m‘ by memory info.

Like System Monitor, you can also use top to kill uncooperative processes. To do this, you’ll need to make note of the process ID you want to kill. Hit the “k” key while top is running, and the utility will ask you to input a process ID number. Input the number, hit Enter, and then hit Enter again when it asks if you want to kill the process (top assumes you mean “yes” when you hit enter). The top utility will then kill the process.

Once you’ve finished with top, hit the q key to exit and return to the command line.

CHECK DISK SPACE USAGE

The top command can do quite a lot, but there’s one thing that System Monitor can do that top can’t – it can show the amount of used disk space. And keeping track of the used space on your hard drive is important. Granted, these days computers come with enormous hard drives - a capacity of one or even two terabytes in a desktop machine is quite common. Of course, the size of popular files has only gotten larger (video takes up an enormous amount of space), making it all the easier to fill up your hard drive. And filling up your hard drive can cause all sorts of unintended problems, especially on a server system.

Fortunately, there are several commands you can use to track disk space usage from the command line in Linux Mint.

The first command is **df**, which produces an output like this:

/dev/sda1 31621016 3364900 26649820 12% /

You'll notice like the Filesystems tab in System Monitor, the df command lists all the filesystems on your computer. The first number is the total size of the drive. The second is the used space. The third is the available space, and the final number is the percentage of space used. However, the numbers are in 1 kilobyte blocks, which makes the difficult to read without mental mathematics. To make the output more readable, use **df** with the -h option:

/dev/sda1 31G 3.3G 26G 12% /

You'll notice that the sizes are now in gigabytes (or megabytes, depending on the size of the filesystem), which is much more readable.

You might also need to check the size of an individual folder, since the ls command, even with the -l option doesn't bother to list the size of folders. (Technically, directories in Linux are also files, so the **ls -l** command only lists the size of the file representing the directory without any of the directory's contents.) To find the size of a folder from the commmand line, use the **du** command with the -s and -h options:

du -sh ~

The command will list the size of the targeted folder in megabytes or gigabytes, as appropriate.

CHECK MEMORY USAGE

The top command does a pretty good job of seeing which processes are using the most memory. It does not, however, give an overview of your system's entire memory. To do so, you need to use the **free** command, which generates an output like this:

Mem: 1025700 340708 684992 0 38904 156368

The first three numbers are the most important - they list the total amount of RAM, the amount used, and the amount currently free. The RAM is listed in bytes which, unless you're really good at mental math, makes it rather hard to read. Fortunately, you can use the -m option with **free** to display the totals in megabytes instead of bytes, generating an output like this:

Mem: 1001 501 500 0 64 277

The numbers are roughly the same as before, but they're expressed in megabytes now, not bytes, which usually makes for easier reading. You can also use the -k and -g switches to express the values in kilobytes and megabytes, if you prefer.

***

## Chapter 8 - Editing Text Files with vi

We've spent the last few chapters covering the basics of Linux Mint - the command line, file permissions, users and groups, and managing system resources. We're now ready to move on to more advanced topics, such as how to configure Linux Mint for a variety of server roles. Linux Mint can be configured to perform almost any server task, offering a powerful server platform at very low cost.

First, however, we have to talk about configuration files, and how to edit them.

Configuration files on the Microsoft Windows platform are almost always *.ini files, or hex files, or binary files that you cannot alter without special programs. In contrast, configuration files on Linux are usually simple text files that you can alter with any text editor program. Linux Mint comes with a graphical text editor, the gedit program, that lets you edit text while providing a full GUI menu with copy and paste and so forth.

However, gedit doesn't work from the command line, and it *definitely* doesn't work in the Server Edition of Linux Mint, which does not include a GUI. Therefore it is vital to learn a command line editor if you want to configure Linux Mint as a server.

There are a number of command line editors available for Linux Mint - nano, Richard Stallman's Emacs, vi, and others. I think vi is the simplest to use, so this chapter will focus on using the vi editor. Granted, opinions can and do differ on the best editor to use - a flame war on the relative merits of Emacs and vi has been going for decades.

WHAT IS VI?

The vi editor has been around for a long time. It grew out of a series of UNIX text editors in the 1960s and the 1970s, with the first version developed by programmer Bill Joy in the late 1970s. Later, vi was praised for its small memory footprint, which meant it could be used on systems with low amounts of available memory.

The variant of vi included with Linux Mint is actually vim, which stands for "vi Improved." Vim was developed by a programmer named Bram Moolenaar in the early 1990s. Today, vim is generally the most popular variant of vi, and is included with most Linux distributions.

However, the vi command is still symbolically linked to vim, so typing vi into Linux Mint's command line will launch vim.

LAUNCHING VI

Launching vi is simply a matter of typing the command:

vi

This will take you to an empty file, and you can create text files from here.

However, you'll often use vi to view or edit an existing text file. If you wanted to use vi to open a file named test.txt:

vi test.txt

The vi editor will then launch with the test.txt file open.

You can also use vi to create new files. For instance, if you wanted to use vi to create a text file named newfile.txt:

vi newfile.txt

However, note that the file isn't actually written to disk (and therefore doesn't exist permanently) until you write it to disk. We'll discuss how to do that in the next section.

VI MODES

Vi is not like a modern word processor, in that you can't simply fire it up, sit down, and start typing. Vi has different modes of operation, each of which has a different function. If you think of vi as a Swiss army knife, then the modes are the different kinds of blades and attachments within the knife.

Vi has four modes:

-Normal mode. Vi starts in default mode, and you can delete text from within normal mode.

-Command mode. This lets you save your text file.

-Insert mode. This lets you type fresh text into your file.

-Replace mode. This is similar to Insert mode, but you can overtype text, which you can't do in Insert mode.

Let's take a closer look at each of the modes.

NORMAL MODE

Vi starts in Normal mode. Normal mode lets you navigate around the text file by moving the cursor with the up and down arrow keys, along with the Page Up and Page Down keys. Pressing the HOME key takes you to the beginning of the file, and pressing END moves you to the end. You can also use Normal mode to delete text within the file, from single characters all the way up to entire lines. Normal mode also offers a search feature, allowing you to quickly locate specific search terms within the file.

First, let's take a look at the commands to delete text within Normal mode.

-Pressing **dw** deletes the word immediately after the cursor. This command also deletes the space following the word.

-Pressing **de** also deletes the word immediately following the cursor. Unlike **dw**, however, it does not delete the space following the word.

-Pressing **d$** deletes from the cursor to the end of the current line.

-Pressing **dd** deletes the entire current line.

-Pressing **p** inserts the text from the last deletion after the current location of cursor. Essentially, in conjunction with the deletion commands, this lets you cut and paste within vi.

-Pressing **u** undoes the last action. Trust me, if you've made a mistake while editing a text file with vi, this can definitely come in handy.

-Pressing **CTRL-G** (the CTRL and the G keys at the same time) displays a status bar at the bottom of the screen. The status bar will display the name of the file, whether or not it has been modified since the last time it was saved, which line and column the cursor currently occupies, and how far into the file you are as a percentage.

-Pressing **/** (forward slash) activates the search function. Type a search term and hit enter, and vi will take you to the first instance of the search term. You can then hit the N key to jump to the next instance of the term.

Once you've deleted items from your text file, you may want to save the changes. We'll show you how to do that next in Command mode.

COMMAND MODE

Normal mode lets you navigate around a text file and delete parts of it, but Command mode lets you save your file. Command mode also lets you quit vi, with or without saving your text file first.

To access Command mode, you must first be in Normal mode. Press the colon key (the : key), and you’ll be moved to Command mode. You’ll know you’re in Command mode when you see a : prompt at the bottom of your screen.

Let’s look at the commands you can use while in Command mode (note that you must hit the Enter key after typing these commands):

-Pressing the **w** key writes the current text file to disk. This basically means that the file is saved. If you used vi to create a new file, it is written to disk. If you’re editing a file, any changes you made to the file are written to the disk. So only use the **w** command if you’re absolutely sure you want to save your changes.

-Pressing the **q** key quits vi and returns you to the command prompt. Note that the **q** command will only work if you haven’t made any changes to the text file, or if you’ve made changes but haven’t yet saved them to disk.

-Pressing the **q!** keys forces vi to quit, even if you haven’t yet written your current text file to disk. This generally gets used when you've made serious mistakes editing a text file and want to start over from scratch. Remember, any changes you made to the text file are discarded, so only use **q**! if you don’t want to save your changes.

-Pressing **wq**, as you might expect, combines the **w** and **q** commands. This command writes your file to disk, and then exits vi.

-Typing exit and then hitting the Enter key does the same thing as **wq**.

INSERT MODE

Insert mode, as the name suggests, lets you insert text into the text file. Access Insert mode by pressing the **INSERT** key while in Normal mode. You can also enter Insert mode by pressing the **I** key or the **S** key while in Normal mode.

Insert mode works much like most people expect a word processor to work – you type, and the text appears on the screen. You can also use the arrow keys and Page Up and Page Down to navigate around the file, even while in Insert mode.

Text is inserted to the right of the cursor. Note that Insert mode doesn’t overwrite text when you type. Any text that already exists is pushed to the right as you add new text.

To return to Normal mode from Insert mode, press the **ESC** key.

Note that you can’t enter Command mode from within Insert mode, since Insert mode interprets the colon character (:) as simply another text character and adds it to the file.

REPLACE MODE

The final mode of vi, Replace mode, works almost exactly like Insert mode, but with one key difference. Replace mode overwrites text as you replace it.

To access Replace mode, press the **INSERT** key while you are in Insert mode. This will shift you to Replace mode. As you type, you’ll notice that preexisting text it overwritten, rather than moved to the right.

Once you’ve finished working in Replace mode, you can return to Normal mode by hitting the **ESC** key.

Note that you can’t enter Command mode from within Replace mode, since Replace mode interprets the colon character (:) as simply another text character and adds it to the file.

WHY LEARN VI?

Compared to graphical editors like gedit, or even graphical word processors like LibreOffice or AbiWord, vi seems hideously complicated. Why learn it?

Because, as we mentioned above, you’ll need it when working from the command line in an environment with no GUI. If you want to use Linux Mint as a server, you’ll need to learn vi (or another command line editor). Besides, vi is actually pretty easy to learn. After some practice, you’ll be editing text files with ease.

***

## Chapter 9 - Network Settings and Assigning a Static IP

The day of the stand-alone personal computer is long past. These days, practically every personal computer, whether a desktop or laptop, will spend most of its life connected to the Internet. Linux Mint is no different. If you want to browse the Internet and check email from a desktop or laptop with Linux Mint, you'll need to connect it to the Internet. And if you have a server running Linux Mint, you'll need to connect it to either the Internet or a local-area network (LAN). Very often you'll need to give a Linux Mint server system a static IP address, as well, so client systems can consistently find it.

In this chapter we'll discuss how to work with IP addresses in Linux Mint, and how to assign a static IP address to your system. Additionally, we'll explain the differences between IP Version 4 and IP Version 6\. IP Version 6 is still dominant, but since the available public IPv4 addresses ran out in 2011, IPv6 will becoming increasingly common in the next few years.

IP VERSION 4 ADDRESSES

First, we should discuss IPv4 addresses. Before we explain how to configure networks in Windows 8, it’s a good idea to have a firm grasp of the basics of IP addressing.

The Internet Protocol is part of the TCP/IP (Transmission Control Protocol/Internet Protocol) suite, a group of related protocols that lay down the rules for how computers communicate over networks, both over LANs (Local Area Networks) and the larger Internet. An IP address, therefore, is a (theoretically) unique 32-bit address assigned to a computer. It's a bit like a street address - it lets other computers send traffic to and receive traffic from your system. An IP address consists of four groups of numbers separated by dots:

192.168.1.1

These numbers are actually the numerical form of a 32-bit binary number. None of these numbers can be higher than 255\. (While watching a detective TV show, it’s occasionally hilarious to see the police track a criminal using a ludicrously implausible IP address, like 689.34.385.339.)

The dominant version of the IP protocol is Version 4, commonly referred to as IPv4\. Under IPv4, there are only 4.6 billion IP addresses available, and the available IP addresses ran out in late 2011\. (IPv6, which has many more available addresses, will eventually replace IPv4, but for now, IPv4 remains dominant.) There are obviously far more computers, phones, routers, switches, and other networked devices in the world than 4.6 billion, so how do all these devices receive IP addresses?

The answer is a "private IP address." Certain blocks of IP addresses have been reserved for use in private networks. These blocks, using a technology called Network Address Translation (NAT), are then "translated" to public IP addresses. This has extended the lifetime of the available IPv4 address space for decades. The ranges of the reserved private addresses are:

10.0.0.0 - 10.255.255.255

172.16.0.0 - 172.31.255.255

192.168.0.0 - 192.168.255.255

Odds are, your computer has an IP address in one of those ranges as part of a private network (even if it's just a private network generated by your wireless router).

Additionally, you might see an IP address that looks like this:

169.254.1.10

An IP address that starts with 169.254 is an Automated Private IP Address, or an APIPA address. APIPA is a feature of Windows systems. When a network connection is active, but has not been assigned a static IP address and cannot contact a DHCP server (more on both of those later in this chapter), Windows automatically assigns itself an APIPA address. This is useful if you have computer on a small network and wish it to communicate with other computers on that network without undue hassle. However, a computer with an APIPA address cannot communicate with the Internet.

One other unique address you might encounter is this:

127.0.0.1

This represents the "local loopback address", and is essentially the IP address the computer uses to identify itself and its TCP/IP software socket. A common troubleshooting step is to see if your computer can communicate with its 127.0.0.1 address. If it can't, that means something is wrong with your computer's TCP/IP software or that the network hardware isn't functioning properly.

SUBNET MASKS

IP address also have a "subnet mask". A subnet mask defines which parts of the IP address designate the network, and which part designates the individual computer on the network. Let's say the IP address of 192.168.1.1 from above has a subnet mask like this:

255.255.255.0

That means the 192.168.1 part of the address indicates the network, while the final 1 indicates the computer.

IP addresses usually include a “broadcast” address. Any traffic sent to the broadcast address is directed to every single computer in the local network. A broadcast address has a “255” as its final number, so a computer with a 192.168.1.1 address will have a broadcast address of 192.168.1.255.

DEFAULT GATEWAY

Lastly, IP addresses usually (but not always) come with a "default gateway". The default gateway is the address your computer sends traffic destined for anywhere outside the local network segment. For example, you visit Google with your web browser. Your computer recognizes that Google isn't on the 192.168.1.* network, and so forwards the request to the default gateway, which then sends the traffic on to Google. (This is a simplification, but adequate for our purposes.)

MAC ADDRESS

Every network adapter also has something called a “Media Access Control” address, or a MAC address. This is an address burned into the physical hardware itself, and is (in theory) unique to each adapter. A MAC address consists of a series of hexadecimal characters separated by colons. For example, 09:00:27:6c:67:34 would be a valid MAC address. MAC addresses are commonly used for network filtering purposes – for instance, you can configure a wireless router to accept only specific MAC addresses as client.

However, this isn't terribly secure, since it's quite easy to spoof or fake a MAC address. Nevertheless, for certain networking applications you will need to know your computer's MAC address.

DNS

The final important piece of basic networking is the Domain Name System, or DNS.

As we mentioned above, every website on the Internet has, in theory, its own unique web address. Remembering all of those IP addresses can prove impractical. A few people might have keen enough memories to remember that microsoft.com has an IP address of 206.46.232.182 (at least at the time of this writing), but most of us cannot.

DNS provides an easier way to find websites. DNS maps each address to a domain name. When you type in a web address, such as microsoft.com or distrowatch.org, your request goes to a DNS server. The DNS server checks its database of domain name mappings (called “zone data”) and responds with the IP address assigned to that domain name. Your computer is then able to contact the website and begin downloading data.

DNS is integral to the smooth functioning of most computer networks. If your computer is suffering connection problems, DNS is one of the first things to check (other than making sure the network cable is plugged in, of course).

A SUMMARY OF IPV6 NETWORKING

As we mentioned earlier, in 2011 the world ran out of available IPv4 address. Since there are only about 4.6 billion IPv4 addresses, and there are far more networked devices in the world than 4.6 billion (think of all those computers, smartphones, tablets, routers, Internet TVs, printers, and other devices), a solution had to be found. Version 6 of the Internet Protocol, IPv6, is that solution. As of this writing, IPv6 is still on the fringes, but in a few years it will supersede IPv4 entirely.

IPv4 used a 32-bit addressing scheme, with four eight-bit groups to identify the computer and the network. IPv6, by contrast, uses a 128-bit binary number for the address. IPv4 maxed out at 4.6 billion available addresses. IPv6 has a theoretical limit of 2^128 addresses. In simple numerals, that's about 340,282,366,920,938,463,463,374,607,431,768,211,456 addresses.

Given that this means we could theoretically assign an IPv6 address to every single atom on the earth, and then have enough addresses left over to assign addresses to the atoms of another hundred Earth-sized planets, it is unlikely that we shall run out of IPv6 addresses anytime soon.

A typical IPv6 address will look something like this:

2001:0db8:85a3:0042:0000:8a2e:0370:7334

However, you will rarely see an entire IPv6 spelled out like this. There are a number of shorthand ways to display an IPv6 address. The first to eliminate any leading zeroes in each of address blocks:

2001:db8:85a3:42:0:8a2e:370:7334

Additionally, you can also use a pair of colons (::) to represent a long string of zeroes. So our original address could be further shortened down to this:

2001:db8:85a3:42::8a23:370:7334

Granted, this is still a lot to type (or to read to a support technician over the phone), but still easier that typing out the entire address.

IPv6 addresses do not have subnet masks the way that IPv4 addresses do. Instead an IPv6 address has a "subnet prefix", which identifies how much of the IPv6 address identifies the local network segment and how much identifies the individual computer. Usually, the first 64 bits of the IPv6 address (the first four blocks of four digits) identifies the network segment, and the second 64 bits identifies the individual computer (and this is usually derived from the computer's MAC address).

There are three main kinds of IPv6 addresses assigned to personal computers. The first is a Global IPv6 address, which is equivalent to a public IPv4 address. Global addresses are designed to be accessible from the Internet, and website or public network services will have a Global address. Global addresses always start with either a 2 or a 3.

A Link-local address is the second major kind of address. A Link-local address basically works the same as an APIPA address, in that a computer assigns itself a Link-local address when it hasn't been given a static address or is able to contact a DHCP server. A Link-local address always starts with fe8.

Finally, the third major kind of IPv6 address given to personal computer is a Site-local address. A Site-local address is equivalent to the private IPv4 addresses we described above. Like IPv4 private addresses, Site-local IPv6 addresses are intended to be used in an organization's private networks, and are usually not accessible from the Internet. Site-local IPv6 addresses always start with fec0\. Not many organizations are currently using Site-local addresses, but as IPv4 becomes increasingly obsolete, more organizations will switch to them.

Like IPv4, IPv6 also offers a local loopback address. The local loopback address for IPv6 is this:

0000:0000:0000:0000:0000:0000:0000:0001

But remember that a string of zeroes can be shortened with a pair of colons. So the local loopback address for IPv6 is usually displayed like this:

**::1**

That is much easier to type!

FIND YOUR IP ADDRESS

It's actually much easier to find your IP address from the command line in Linux Mint than from the graphical interface. Simply go to a command prompt and type this command:

ifconfig

The ifconfig command will generate an output that looks something like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_558379d3.jpg)

There's quite a bit of information here, but most of it is useful. The "eth0" refers to the first Ethernet connection on your system. The "indet addr" displays your system's IP address, while "Mask" shows the subnet mask. "HWaddr" shows your Ethernet adapter's MAC (Media Access Control) address, which is (theoretically) unique to each adapter. (Some wireless networks require you to supply your MAC address before allowing your system to connect.)

You can pipe the output from the ifconfig command to grep to quickly find the specific item you want. Let's say you just want to find the IP address:

ifconfig | grep inet

This time, the output will look like this, and you can quickly pick your IP address from the mix:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_1df91bf7.jpg)

Likewise, you can quickly find your computer's MAC address with ifconfig and grep:

ifconfig | grep HWaddr

You can easily pick out your MAC address from the output:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m368c6e.jpg)

How do you find your system's default gateway? You need to use another command for that:

ip route

The ip route command will spit out an output like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_m44ce4bfb.jpg)

Look for the line that begins "default via." Your system's default gateway will be the IP address after those two words.

Now that you know how to find your IP address, let's talk about how to actually obtain an IP address for your Linux Mint system.

GETTING AN IP ADDRESS FROM DHCP

Most of the time, your computer will receive an IP address from a DHCP server.

Configuring each individual computer with an IP address by hand is time-consuming and error prone; if one or more computers receive the same IP address, they won't be able to connect due to the address conflict. DHCP, which stands for "Dynamic Host Configuration Protocol", takes the guesswork out of the process. When a computer plugs into a Ethernet network (or connects to a wireless network), it sends out a request for a DHCP server. If there's a DHCP server on the network, it supplies the computer with an IP address, and the DHCP server ensures that no two computers receive the same IP address.

Most of the time, when you plug into a new network, you'll receive a DHCP address automatically. If you don't, however, try this command:

sudo dhclient

This will manually tell your system to search for a DHCP server and accept an address. If this command doesn't work, that means either the network you're using doesn't have a functioning DHCP server, or that something is blocking the DHCP server from communicating with your computer.

RELEASING A DHCP ADDRESS

DHCP addresses come with a "lease", which means the amount of time your computer is allowed to keep the address. Usually, your computer will contact the DHCP server at the halfway point before the lease expires, and ask for permission to keep it, which the DHCP server almost always grants.

Sometimes you want to release a leased IP address early - like if your network's DHCP server changes, or if your computer refuses to release its IP address. You can do this with the dhclient command and the -r option:

sudo dhclient -r

This releases your IP address, and you can then use sudo dhclient to contact a DHCP server to receive a new one.

SET A STATIC IP FROM THE GUI

DHCP address are convenient, but they have one big weakness - they can change quickly. If the lease length is short enough, your IP address could be 192.168.1.1 on Monday and 192.168.3.45 on Tuesday, depending on which addresses the DHCP server happens to have available. For laptop and desktop computers this normally isn't a big deal. Servers, however, need to have consistent IP addresses so client computers can locate them.

This is where a "static IP" address comes in. A static IP is one that you manually assign to a computer, one that it keeps forever or until you change it. You'll need to make sure that it doesn't conflict with your DHCP server, so you'll need to either reconfigure your DHCP server to exclude the static address from its address pool, or ask your system administrator to do it.

Here's how to set a static IP for your system's Ethernet adapter from the GUI.

-Launch Network Connections by clicking on the mintMenu and searching for it in the search field.

-When the Network Connections dialog box opens up, click on the Wired tab, and then on the connection labeled eth0\. Click on the Edit button.

-When the Editing eth0 box opens up, click on the tab for IPv4 Settings.

-In the IPv4 box, change the Method drop-down box from Automatic to Manual.

-Under the Addresses heading, click the Add button to add a static IP, subnet mask, and default gateway.

-Add your DNS server to the DNS Servers line.

-Click OK.

This is kind of an involved procedure - I think it's easier to set a static address from the command line, which we'll cover in the next section.

SET A STATIC IP

To set a static IP address from the command line in Linux Mint, you'll need to edit a pair of text files - specifically /etc/network/interfaces and /etc/resolv.conf. Time to break out those vi skills you learned in the last chapter! Only root has permission to edit the files in question, so you'll need to use sudo in conjunction with vi to make this work.

First, make a backup copy of the interfaces file:

sudo cp /etc/network/interfaces ~

This will make a backup copy in your home directory. Why make a backup copy? Before editing any configuration file in Linux Mint, it's always a good idea to make a backup copy in your home directory. That way, if something goes wrong, or you make a mistake, you can quickly restore the backup copy and get your system in working order again.

Next, open up the interfaces file in vi:

sudo vi /etc/network/interfaces

Initially, the file only contains information about your local loopback address. (The local loopback address is 127.0.0.1\. It doesn't go anywhere, and it's used to test if your computer's TCP/IP stack is working properly):

**auto lo** 

iface lo inet loopback

To give your system a static IP address, you’ll need to make some changes to this file.

Let’s say you want to assign a static IP of 192.168.1.2 to your eth0 network connection (which, as you'll recall, is the first adapter on your system - additional adapters will be numbered eth1, eth2, and so on), with a subnet mask of 255.255.255.0 and a local gateway of 192.168.1.1\. Switch vi over to Insert mode and add the following lines:

auto eth0

iface eth0 inet static

address 192.168.1.2

netmask 255.255.255.0

broadcast 192.168.1.255

gateway 192.168.1.1

Once you’ve added these lines, enter Command mode in vi, and save and quit (you can do this with either the **qw** or the **exit** commands). You've added your static IP, subnet mask, and default gateway, but you'll still need to add a DNS server, and you can do that by editing the /etc/resolv.conf file:

sudo vi /etc/resolv.conf

To set a static DNS server with the address of 192.168.1.10, switch vi to Insert mode add this line to the file:

nameserver 192.168.1.10

Save the file, and exit your text editor.

You’ll then to need have your system load the new IP configuration. You can do that by rebooting, but if that takes too long, you can use this command to force Linux Mint to re-read the configuration files:

sudo ifup eth0

Your system will then have a static IP address.

***

## Chapter 10 - Basic File Sharing with Samba

One of the most common uses of a Linux Mint machine – whether a server or a desktop – is to share files across the network. If you’re not familiar with the term, “file sharing” means to make a folder on your system available to clients on the network. From their own machines, users are able to access your shared folder from their computers, and depending upon how you’ve configured the security, they can copy the files for themselves, alter the files, add new files, or even delete files.

There are a number of different programs that offer file-sharing capabilities. Most Linux Mint systems use the “Samba” software, since it is can easily share files with Windows-based computers. It’s common to find organizations that have a number of users with Windows systems storing their data on a Linux server running Samba.

WHAT IS SAMBA?

Samba gets its name from the Server Message Block / Common Internet File System protocol, which is usually abbreviated to SMB/CIFS. A programmer named Andrew Tridgell first started developing what would become the Samba server in 1991 and 1992\. Initially he called the project "smbserver", but later he received a trademark notice from a company that owned the rights to that name. To find a different name, Tridgell searched the UNIX system dictionary for words containing the letters "s, m, b", and settled upon Samba.

Samba quickly became popular because it allowed easy file sharing between UNIX-based, and later Linux-based, computers and Windows systems. Today, Samba is widely used, and Windows, Mac OS X, and Linux clients can all access files on a Samba share.

We'll show you how to set up a basic Samba server, and how to access those shares from client computers.

BASIC SAMBA SETUP

Samba has a vast array of options and configuration settings, but here we'll show you how to set up and configure a basic Samba server with one user.

First, you’ll need to install Samba. Make your way to a command prompt and type this command:

sudo apt-get install samba

Enter your password to authenticate, and **apt** will download and install Samba and its attendant utilities for you.

In Chapter 3 we talked about Linux Mint's user accounts, noting that they're stored in the /etc/passwd file. A key thing to understand about Samba is that it stores its own set of user accounts, separate from the main accounts, in the /etc/samba/smbpasswd file. That means you'll need to create a separate Samba password for every user you want to access your file shares. You create this password using the **smbpasswd** command. Using the camalas account for Caina Amalas that we created in Chapter 5, here's how the command should look:

sudo smbpasswd -a camalas

Be sure to give camalas's Samba account an appropriately strong password (including uppercase, lowercase, punctuation, and numbers). Once camalas's password is created, the next step is to create a directory for her to share. Begin by creating a folder named 'test' in camalas's folder, which we'll use for our first shared folder:

mkdir /home/camalas/test

(NOTE: *DO NOT* use sudo to create the folder, because then the owning user and group will be set as ‘root’, which means you won’t be able to access the folder using your Samba username and password.)

The next step is to edit the /etc/samba/smb.conf file, the main configuration file for Samba. As always, make a safe backup copy of the original smb.conf file to your home folder, in case you make an error:

sudo cp /etc/samba/smb.conf ~

Now use vi to edit the /etc/samba/smb.conf file:

sudo vi /etc/samba/smb.conf

The smb.conf file is long and rather complex, but for the purposes of this demonstration, you can ignore most of it. Key down to the very end of the file and insert this text:

[test]

path = /home/camalas/test

available = yes

valid users = camalas

read only = no

browseable = yes

public = yes

writable = yes

(There should be no spaces between the lines, and note also that there should be a single space both before and after each of the equal signs.)

Here's what some of the more important configuration options mean.

-The "[test]" gives the name of the file share.

-The "path" option specifies the location of the folder to be shared.

-The "available" option specifies that the file share is available to clients on the network.

-The "valid users" option details the users that are allowed to access the file share. In this case, we've set it so that only the camalas account can access it. You can add additional accounts here, if you prefer.

-The "read only" option specifies whether nor not clients will be allowed to write to the file share.

-The "writable" option specifies that data can be written to the file share.

The settings specified above will share the test folder we created earlier, and give the camalas username and the camalas username alone permission to read and write to the folder. Once you have input the changes, save smb.conf, exit vi, and restart Samba with this command:

sudo /etc/init.d/samba restart

(This will force Samba to restart, re-reading its configuration files and activating the share you just created.)

Once Samba has restarted, use this command to check your smb.conf for any syntax errors:

sudo testparm

If you pass the testparm command, Samba should be working. Try accessing the share from another client on your LAN.

We'll explain how to do that before the end of the chapter.

ACCESSING SHARED FOLDERS FROM A Linux Mint CLIENT

If you followed the directions in the previous section, you should have a working Samba server on your Linux Mint system.

Accessing the file share from another Linux Mint system is simple enough, using the GUI. To access the share from a client Linux Mint system, go to the Go menu, and then select Connect to Server. When the Connect to Server dialog box opens, select Windows share. The dialog box will change with additional options. Put in your Samba server's IP address in the Server line, and hit connect. An icon for the server should then appear on the desktop. Double-click the icon, and you'll be asked for a username and password. Put in the username and password of the account that has access to share, and you should have access to it.

To access the file shares from a command-line client takes a little more work.

First, you’ll need to install the **cifs-utils** and the **smbfs** packages on the client system. Go to a command prompt and type this command:

sudo apt-get install cifs-utils smbclient

Enter your password to authenticate, and **apt** will download and install those packages for you. Once the packages are installed, you can use them to connect to a Samba server.

Now, to continue our previous example, let's say that you followed all the walkthroughs in the previous chapter, which means you have a Linux Mint server running Samba with an IP address of 192.168.1.2, hosting a shared folder called "test". You created the camalas account, and let's say you assigned that account a password of "ghost". You want to access that file share from a client computer.

First, query the Samba server to see what shares are available with this command:

sudo smbclient -L 192.168.1.2

This will display a list of any shares available on the Samba server. You should see the test share available.

Now let’s say you actually want to connect to the “test” share on 192.168.1.1\. First, you’ll need a “mount point”, a place in your client computer's filesystem where it can mount the Samba share as a directory. If you don’t already have a mount point, you can make one with this command:

mkdir ~/mount

This will generate a directory called mount in your home folder. We’ll use it in the next command to mount the Samba share.

To actually mount the Samba share, use this command:

sudo mount //192.168.1.2/test ~/mount -o username=camalas,password=ghost

This will mount the shared directory “test” on 192.168.1.1 in the “mount” folder we just created in the client’s home directory.

To unmount the shared folder, simply use this command:

sudo umount ~/mount

This will dismount the file share from your client computer.

Note that the command is in fact actually spelled “umount”, not “unmount” – accidentally typing "unmount" for the **umount** command is a common typographical mistake.

ACCESSING SHARED FOLDERS FROM A WINDOWS CLIENT

Generally, connecting to a Samba share on Linux Mint machine from a Windows client should be straightforward. However, there are a few pitfalls to beware.

Let's assume that you've stuck with the settings we've used already, and you now have a Linux Mint Samba server with an IP address of 192.168.1.2 (and a subnet mask of 255.255.255.0). The server hosts a share called "test", and the user account "camalas" has access with a password of "ghost." You want to connect to this share from a Windows machine with an IP of 192.168.1.3 and a subnet mask of 255.255.255.0.

On the Windows machine, go to Start menu, and then to Run (or hit the Windows Key and R simultaneously), and type this into the Run box:

\\192.168.1.2

Alternately, you can also type this into the address bar in any Windows Explorer window. This is what's called an UNC path - a "Universal Naming Convention" path.

Unless you have a DNS server set up, it’s better to use the IP address instead of the hostname to access your Linux Mint machine from Windows. In fact, if you don’t have a DNS server set up, you’ll *have* to use the IP address to get to the Samba server from your Windows machine, since your Windows machine won’t be able to resolve the Linux Mint’s IP address. Giving your Linux Mint machine a static IP address, as we discussed in Chapter 7, would make this easier.

Click OK if you typed the UNC into the Run box, or hit the Enter key if you typed it into Windows Explorer, and you should receive a username and password prompt for the share. Using the example above, enter your username and password in this format:

camalas@192.168.1.2

ghost

It’s necessary to enter the username as “**camalas@192.168.1.2**″ (or as **192.168.1.2\camalas**, alternately), because otherwise Windows tries to authenticate the Samba share against its own accounts. That, of course, will not work. Using the IP address in the account name forces Windows to authenticate against the Samba server.

If that doesn’t work, first make sure you’ve typed the username, the password, and the IP address correctly. One mistake and it won’t work, and the password IS case sensitive. Next, check the /etc/samba/smb.conf file to make sure the share permissions are set correctly. Also check the filesystem permissions and ownership of the folder you are trying to access. Your user account will need to have permission to actually get at the share folder, regardless of the share permissions. If you created the share folder using sudo, for instance, the root user and the root group will have ownership of the folder, and you won’t be able to get at it using your Samba account.

***

## Chapter 11 - FTP Client and Server

FTP stands for "file transfer protocol", and it allows you to transfer files to a remote computer. FTP has been around forever, and it has a number of pros and cons. Since FTP is so old, it is supported on virtually every operating system, and most operating systems include an FTP client of some kind. The downside is that FTP is not terribly secure. It has a bad habit of rotating ports, which makes it hard to use across the Internet (firewalls really don't like having ports change on them abruptly), and an FTP server that allows for anonymous login is tremendously insecure - anyone can upload or download material, which means that an FTP server that allows anonymous access can quickly find itself hosting illegal material. (These days, FTP servers that allow anonymous access are quite extremely rare.) I strongly prefer to use SFTP instead, which we will discuss in Chapter 11.

However, Linux Mint can act as an FTP server with a reasonable degree of security. In this chapter, we'll show you how to set up Linux Mint as an FTP server, and how to use a command-line FTP client.

INSTALL AND CONFIGURE AN FTP SERVER

The most common FTP server software for Linux Mint is the vsftpd package, which stands for "very secure FTP daemon." It's the default FTP package for Linux Mint, and most other Linux distributions as well. As an added bonus, vsftpd is pretty secure out of the box - to make it insecure, you have to go out of your way to mess up the configuration file.

As an added bonus, vsftpd is simple to install and configure on a Linux Mint machine. To install the vsftpd package, make your way to a command prompt and type this command:

sudo apt-get install vsftpd

Enter your password to authenticate and **apt** will download and install vsftpd for you.

Follow the default prompts, and the vsftpd server will be installed on your computer. Generally, the default configuration for vsftpd is pretty secure, and good enough for casual use. Anonymous users are blocked, and no one can write files to the server (or, in FTP terminology, no one can upload files to the server). Anyone with a system account will be able to connect to the FTP server and download, though not upload, files.

If you want to change any settings, the configuration file for vsftpd is /etc/vsftpd.conf. Like any other configuration file, you can edit it with vi:

sudo vi /etc/vsftpd.conf

Like Samba, the vsftpd.conf file contains a large number of "directives" that govern how the server behaves and operates. If you want to change its configuration, you'll need to alter the directives.

If you want users to be able to write files to your FTP server, change this directive:

#write_enable=YES

To this:

write_enable=YES

With the write_enable directive set to YES, users will be able to upload files to your FTP server. Note, however, that they will only be able to do so if they have proper permissions to the directories in question. They'll be able to upload files to their home directories, but not, for instance /var or /usr.

Anonymous access is controlled with this directive:

anonymous_enable=NO

*Under no circumstances should you allow anonymous access to your FTP server, especially if it is accessible from the Internet!* There are certain circumstances when you might find it useful, but you should only enable it if you know *exactly* what you are doing. Generally, it is almost always best to keep **anonymous_enable** set to NO.

If you make any changes to the file, switch vi to command mode, save the changes, and then exit vi. Then restart the vsftpd server so it reads its new directives:

sudo service vsftpd restart

You can then test your Linux Mint machine’s FTP service from the server's command line:

ftp 127.0.0.1

The FTP client will ask for your username. Enter that, and then the client will ask for your password. Enter that as well, and you should then see the FTP prompt, which looks like this:

ftp>

If you see that, you know the server is working. You can return to the regular command line with this command:

exit

USING THE FTP CLIENT

Just because you have an FTP server doesn't mean you can access it straightaway - you first need a program called an "FTP client" that will let you communicate with the FTP server. Fortunately, Linux Mint comes with a built-in FTP client - you can access it from the command line by simply typing:

ftp

However, it's far easier to use if you know the IP address of the FTP server you want to access. Let's say you want to access a FTP server with an IP address of 192.168.1.100\. To do so, you would append the IP address to the ftp client command:

ftp 192.168.1.100

The FTP client will then ask for your username. (Note that this will be your username and password on the FTP server, not your username and password on the computer with the FTP client.) Type it and hit enter. The client will ask for your password, which you should then enter. Once you do, you'll be taken to the FTP prompt, which looks like this:

ftp>

You can also specify a different username as part of the ftp command. If, for instance, you wanted to use our camalas account to connect to the FTP server at 192.168.1.100, the command would look like this:

ftp camalas@192.168.1.100

Once at the FTP prompt, you can use some of the common terminal commands. To see a listing of the remote directory, you can use the ls command:

ls

This will display the contents of the remote directory.

To find which remote directory you're actually in, you can use the pwd command:

pwd

This command, as you might remember from Chapter 1, stands for "print working directory", and will display the current working directory.

To download files from the FTP server, you will need to use the **get** command. For instance, to retrieve a file named "report.doc" from the current working directory:

get report.doc

This will download the file to your local home directory.

To upload files to the FTP server (assuming that the server's write_enable directive is set to YES), you'll need to use the **put** command. To put a file named "data.doc" on the remote server:

put data.doc

This will upload the file to the remote directory on the FTP server.

This is only a basic overview of the commands available with the FTP client - many more are available. Also, if you would prefer to use a graphical FTP client, I would recommend the excellent Filezilla client, which you can install with this command:

sudo apt-get install filezilla

***

## Chapter 12 - Using SSH and SFTP

SSH stands for "secure shell", and it is a network protocol that allows you to securely send commands to a remote machine. We discussed in Chapter 3 how a "shell" is a program that provides an interface between the user and the operating system. SSH is a "remote" shell that allows you to send commands to a machine over the network. The "secure" part comes from the fact that the connection is encrypted, which means that an attacker cannot eavesdrop on the connection, or intercept and replace your commands with his own midway through transit. SSH is pretty reliable and secure, and is commonly used in the Linux world. Administrators often use it to remotely manage machines – it’s usually more comfortable to control a server from your laptop than in the chilly and noisy server room.

SSH also offers the SFTP protocol, which stands for "SSH File Transfer Protocol". Basically, SFTP is similar to the FTP protocol, but it uses SSH's security functions to encrypt the connection. That means SFTP is much more secure than FTP.

In this chapter, we'll show you how to set up an SSH server, how to use the SSH command-line client, and how to use SFTP. We'll also show you how to set up SSH to use key-based authentication, which is much more secure than password-based authentication.

INSTALL AND CONFIGURE AN SSH SERVER

Linux has always had strong support for SSH, and Linux Mint is no different. In this section, we’ll walk through a basic installation of an SSH server, and some basic security configuration as well. The default SSH server package for Linux Mint is OpenSSH Server, which we’ll use here.

First, you’ll need to install OpenSSH Server. To do so, open up a Terminal window and type the following command:

sudo apt-get install openssh-server

Enter your password to authenticate, and the **apt** utility will download and install OpenSSH Server for you. Depending on the speed of your Internet connection and your computer, the installation may take several minutes.

Once the installation has finished, return to the Terminal window. We’ll need to make a few changes to your /etc/ssh/sshd_config file in order to increase SSH’s security. First, as always, we’ll want to make a backup copy of your sshd_config file in case anything goes wrong. Type this command into the Terminal:

sudo cp /etc/ssh/sshd_config ~

This will make a backup copy of the sshd_config file in your home directory.

Next, we’ll need to edit the sshd_config file itself. So it’s time to use your skills in vi again:

sudo vi /etc/ssh/sshd_config

Like almost every other server software package, SSH is controlled by a number of directives in its configuration file. The default installation of OpenSSH server is reasonably secure. However, you might want to make a few changes to tighten up its security to additional degree.

The “PermitRootLogin” directive is one you’ll want to change. Once you’re editing the /etc/ssh/sshd_config file, you’ll want to change the following directive as follows:

PermitRootLogin no

This will keep anyone from attempting to log into your server via SSH as root. It’s generally a good idea not to allow any to log into your SSH server as root. If an attacker manages to hack into your SSH server with the root login, he will have complete control over your machine, and that is definitely not a good thing.

Another directive you might want to change is the “AllowUsers.” When the AllowUsers directive is active, only users specifically specified in the directive can access the system through SSH. This adds an additional layer of protection to your SSH server by only allowing specific users to connect via SSH. For instance, if you wanted to limit SSH access to just the “camalas” user account, edit the AllowUsers directive like this:

AllowUsers camalas

To add multiple users to the AllowUsers directive, just add them one by one without commas or semicolons. An AllowUsers directive that permits the camalas user account and the lmaraeus user account to log in would look like this:

AllowUsers camalas lmaraeus

You may also want to consider changing the Port directive. By default SSH runs over TCP/IP port 22, which means that any malware bot autoscanning port 22 can target it. If you set up your user accounts with a weak password (always a bad idea), eventually an automated bot might break through and guess the password. Changing the Port directive to something different will make SSH run over a different port, blocking some of those automated cracking attempts. To set SSH to run over port 5699 instead, make sure your Port directive looks like this:

Port 5699

Note that if you change your SSH server’s default port, you’ll need to remember the new port number when using an SSH client, which we’ll cover in the next section.

After you’ve finished changing the directives in /etc/ssh/sshd_config, switch vi to command mode, and save and quit vi. After you return to the command line, restart the SSH daemon with this command:

sudo /etc/init.d/ssh restart

You should now be able to SSH into your Linux Mint machine from another system with an SSH client.

CONFIGURE SSH TO USE KEY-BASED AUTHENTICATION

SSH is pretty secure, but it does have one weak link – the password. If someone cracks your SSH password, they can gain control over your SSH server.

A more secure method of SSH logons is to use a public/private key. With a public/private key, you create a matched pair of private and public keys. You keep the private key on your personal machine, while you put the public key on the SSH server to which you wish to connect. When configured in this manner, the SSH server will only allow connections from systems that have a matching private key for one of the public keys.

In this section, we’ll show you how to set up key-based logons for SSH.

First, install OpenSSH server on your server. For the rest of this walkthrough, we’ll assume that you installed the SSH server on a machine with the IP address of 192.168.1.100, and that you intend to connect to that server from a client machine with the IP address of 192.168.1.200.

After SSH server has been installed, go to your client machine at 192.168.1.200 and enter this command:

**ssh-keygen -t dsa**

Press Enter, and the command will save a matched public/private key in the ~/.sshdirectory. Specifically, it creates two files – id_dsa, which is your private key, andid_dsa.pub, which is your public key. It will also ask you to set a passphrase for the use of the key, which is an additional layer of security in case someone gains access to your account. Setting a passphrase is usually a good idea.

After the command is complete, you’ll need to transfer the newly created id_dsa.pubpublic key file to your SSH server at 192.168.1.100. Once you have moved it to your server, copy the file to your user account’s ~/.ssh directory on the server. (If this directory does not already exist, create it with the mkdir command.) Next, change to the~/.ssh directory, and use this command:

**touch authorized_keys**

This will create a file to store authorized keys in the ~/.ssh directory. Use this command to add your public key to the authorized_keys file:

**cat id_dsa.pub >> authorized_keys**

Finally, use the chmod command to make authorized_keys read-only to protect from accidental deletion:

**chmod 400 authorized_keys**

Finally, you’ll need to alter your SSH server’s configuration file to mandate key-based logins, otherwise the server will continue to allow password-based login. Use the vi editor to edit SSH’s main configuration file:

**sudo vi /etc/ssh/sshd_config**

Once editing the file, make sure the PasswordAuthentication directive is set to no. This will force your SSH server to only allow key-based login attempts. After you’ve finished editing the file, restart your SSH server with this command:

**sudo service ssh restart**

Your SSH server will not only permit key-based logons – users must have a private key that matches with a corresponding public key in their ~/.ssh/authorized_keys file in their home folder on the SSH server.

Make sure to back up your private key in a safe place – if you lose it, you will lose access to the SSH server.

USING AN SSH CLIENT

Almost all Linux distributions, including Linux Mint, come with a command-line SSH client. Once you successfully connect to an SSH server, it’s as if you were sitting front of that machine, using a command line session. You can issue commands, move and delete files, and run programs, limited only by your permissions on the SSH server.

Let’s say you want to connect to an SSH server with the IP address of 192.168.1.100\. To do so, you would simply use the ssh command at the command line to launch the SSH client:

ssh 192.168.1.100

The first time you connect to a new SSH server, the client will display the server’s RSA fingerprint (RSA is a kind of encryption), and will ask if you want to continue connecting. Type out “yes” and hit enter (just hitting “y” won’t work). The SSH client will then ask for a username and password, and assuming you type those correctly, you’ll be in. You can then start using the remote machine as if you were sitting in front of it.

However, you might want to skip a step. With the addition of the –l switch, you can specify a username with the ssh command. In this example, the SSH client will attempt to connect using the “camalas” username:

ssh –l camalas 192.168.1.100

You’ll only need to enter the password for camalas’s account to connect.

By default, the SSH client attempts to connect using Port 22. However, if you used the Port directive in your SSH server’s /etc/ssh/sshd_config file to change the default port, your SSH client won’t be able to connect, and will come back with an error message. In our example above, we set the SSH server to listen on the 5699 port. To tell the SSH client to connect using that port, use the –p switch:

ssh –p 5589 192.168.1.100

You can also combine that with the –l switch as well:

ssh –p 5589 –l camalas 192.168.1.100

This will make the ssh client attempt to create an ssh connection to 192.168.1.100 using port 5589 and the camalas user account.

USING SFTP

SFTP, as mentioned above, is basically the File Transfer Protocol run over an SSH connection. Since it uses SSH’s encryption, it’s much more secure than traditional FTP. As an added bonus, there’s no need to set up a separate SFTP server – the OpenSSH Server package includes a built in SFTP server, which is also governed by the /etc/ssh/sshd_config file. Like with an FTP server, you need an SFTP client – but Linux Mint (and most Linux distributions) include one by default.

You can access the SFTP client from the command line by simply typing:

sftp

However, it's far easier to use if you know the IP address of the SSH server you want to access. Let's say you want to access a SSH server with an IP address of 192.168.1.100\. To do so, you would append the IP address to the sftp client command:

sftp 192.168.1.100

The SSH client will then ask for your username. (Note that this will be your username and password on the SSH server, not the computer with the SFTP client.) Type it and hit enter. The client will ask for your password, which you should then enter. Once you do, you'll be taken to the SFTP prompt, which looks like this:

sftp>

You can also specify a different username as part of the **sftp** command. If, for instance, you wanted to use our camalas account to connect to the SSH server at 192.168.1.100, the command would look like this:

sftp camalas@192.168.1.100

If you set up the SSH server to listen on a different port than the default of port 22, you’ll need to tell the SFTP client to use a different port with the “-P” switch. Note that this is different than the SSH client, which uses the “-p” switch – remember that the Linux command line is case-sensitive. To make the SFTP client use the 5589 port, the command should look like this:

sftp –P 5589 192.168.1.100

Once at the sftp prompt, you can use some of the common terminal commands. To see a listing of the remote directory, you can use the ls command:

ls

This will display the contents of the remote directory.

To find which remote directory you're actually in, you can use the pwd command:

pwd

This command, as you might remember from Chapter 3, stands for "print working directory", and will display the current working directory.

To download files from the SSH server, you will need to use the **get** command. For instance, to retrieve a file named "report.doc" from the current working directory:

get report.doc

This will download the file to your local home directory.

To upload files to the SSH server, you'll need to use the **put** command. To put a file named "data.doc" on the remote server:

put data.doc

This will upload the file to the remote directory on the SSH server.

THE SSH CLIENT ON WINDOWS AND MACINTOSH MACHINES

Now that you have your Linux Mint machine set up as an SSH server, you might want to know if you can connect to it from a Windows or a Macintosh system.

The answer is yes! The Mac, in particular, makes it easy. Mac OS X is a version of UNIX, and if you remember the introduction, Linux and UNIX are closely related. The Mac has both a built-in SSH client and an SFTP client which you can use from the Mac OS X Terminal utility. (Terminal is the Utilities folder in the Mac’s Applications folder.) Additionally, you can also set up a Mac machine as an SSH server. If you go to System Preferences, and then the Sharing control panel, you can check “Remote Login” to enable the Mac to act as an SSH server. From the Sharing control panel, you can also select the users allowed to SSH into the Mac.

Windows comes with no-built in SSH capability. However, a number of SSH clients are available for the Windows platform. My favorite is the PuTTY client, which can act as both a Telnet and an SSH client. If you need an SFTP client for Windows, the redoubtable graphical program FileZilla (which we mentioned with Linux Mint’s FTP server) can act as an SFTP client, and it’s available for Windows.

***

## Chapter 13 - Install and Configure Apache Web Server

For both good and for evil, the Internet has revolutionized how people communicate, buy goods and services, read books, listen to music, and find friends and potential spouses. The very existence of this book is a testament to the power of the Internet – after all, you probably bought this book from a site selling eBooks, and the Linux Mint install disc is downloaded over the Internet. In point of fact, this book only exists at all because of the Internet – almost certainly no paper publisher would put out a short introductory book on Linux Mint (let alone one written by a fantasy author!).

At the heart of the Internet revolution is a piece of software called a web server. What a web server does is host HTML documents called web pages, which are then served up to client web browsers across the World Wide Web. Web pages can range from simple static HTML pages to elaborate web apps providing banking, commerce, and social networking functions.

Linux might not have the desktop share of Microsoft Windows, but it dominates the web server market. Between 33 to 40 percent (depending on who’s doing the counting) of web servers are Linux/UNIX/UNIX-like machines running a program called Apache HTTP Server, most commonly referred to as just “Apache.” Apache has been around since 1995 or so, and its development has fueled the growth of the World Wide Web.

You can easily install Apache on a Linux Mint system. A Linux Mint machine can serve as a web server for simple static HTML pages, and can scale up to supporting large and complex web applications. In this chapter, we’ll show you how to set up a simple Apache server. In later chapters, we’ll build on that install to run some more powerful web applications, like WordPress and MediaWiki.

INSTALL APACHE WEB SERVER

As installations go, installing Apache on Linux Mint is a breeze. (Configuring it, of course, is substantially more difficult.) To install Apache, type this command at a Terminal window or a command prompt:

sudo apt-get install apache2

(Technically, you’ll be installing Apache 2, the latest version.)

Enter your password to authenticate, follow the default prompts, and apt will download and install the Apache web server for you.

And that’s it! Apache should now be working. To test it from the web server itself, go to a web browser and visit the address http://127.0.0.1\. You’ll remember that this is the “local loopback” address, basically the IP address the local computer uses to refer to itself. Alternatively, you could test it from another computer on the same subnet. For instance, if you installed Apache on a computer with an IP address of 192.168.1.100, you could test it by going to another computer on the same subnet and visiting http://192.168.100 from the web browser.

Regardless, if Apache is working properly, you should see the default Apache/Linux Mint web page with the Linux Mint logo in the upper left-hand corner.

Apache is now operational. In the next section we’ll talk a little bit about configuring Apache.

BASIC APACHE CONFIGURATION

Apache configuration can get extremely complex, depending on the scale of the website involved. A full overview of Apache configuration is way beyond the scope of this book – indeed, dozens of excellent books have been written on the topic. However, here we can take a brief look at Apache configuration.

Apache’s chief configuration file is /etc/apache2/apache2.conf. (In some Linux distributions, it’s /etc/apache2/httpd.conf, but Linux Mint uses /etc/apache2/apache2.conf.) You can look around in the file using **vi**, **cat**, or **less**, but it’s generally a good idea to change things only if you know what you’re doing. And as always, make sure to create a backup copy of a configuration file in your home directory before you alter it, in case something goes irretrievably wrong.

Linux Mint stores your actual web files (the HTML files that make up your website) in the /var/www/html directory. After an installation of Apache, there’s only one file in that directory – the index.html file, which contains the “it works!” message we saw earlier. Otherwise the directory is empty. You can put your own HTML files in here. Coding HTML is beyond the scope of this book, but remember that you’ll need to create your own index.html file once you build your own site.

However, loading HTML files into the /var/www/html directory will only allow you to create a static website. If you want a dynamic website, once that updates content, you’ll need a database backend – and we’ll discuss that in the next chapter. In the next section of this chapter, we'll show you how to set up Apache to use virtual hosts.

VIRTUAL HOSTS

As we've discussed in the previous section, it is easy to set up a simple web server with Apache. However, you might need a more complex web server, one that can host multiple separate websites, rather than subdirectories within a larger website.

How do you do this?

Apache has a feature called “virtual hosts” that lets you run separate websites, with completely different domain names, on the same physical server. Fortunately, implementing virtual hosts for Apache is actually quite simple to do. In this example, we’ll show you how to set up a new website called “examplename.com” on an Apache web server.

First, you’ll need to set a location for your new web site’s files. Apache, you might recall, by default stores the web files in /var/www/html. For this example, create a new folder for the website with this command:

**sudo mkdir /var/www/html/w2**

Next, you’ll need to create a configuration file for the new website in the /etc/apache2/sites-available directory. Fortunately, that directory contains a default file you can simply copy and use as a template with this command:

**sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/examplename.conf**

(Make sure to include .conf extension. Linux Mint 14.04 Trusty Tahr and above run Apache 2.4, which requires it.)

The next step is to edit the new configuration file with the correct settings. You can do this using the **vi** text editor:

**sudo vi /etc/apache2/sites-available/examplename.conf** 

(We discussed how to use **vi** back in Chapter 6.)

Once editing the file with **vi**, you’ll need to make a few changes.

Change the “Document Root” directive from /var/www/html to the proper location of your new website, in this case, /var/www/html/w2.

Also change the “Directory” directive from /var/www/html to /var/www/html/w2.

Finally, under the line that begins “ServerAdmin”, add a new line for the new website’s domain name. For our website named “examplename.com”, add a line like this:

**ServerName examplename.com**

Save changes to the configuration file, and then exit **vi**.

Now you’ll need to modify Apache to display the new domain names to web visitors. Fortunately, you can do this with the a2ensite command:

**sudo a2ensite examplename.conf**

(Note that “examplename” would change depending upon what you named your configuration file.)

One final step – restart Apache to force it to re-read its configuration files and start serving the new website:

**sudo /etc/init/d apache2 restart**

Make sure you have some sort of index.html file in /var/www/html/w2, and the examplename.com website should now be working.

***

## Chapter 14 - Install and Configure MySQL Server and phpMyAdmin

You’ve probably heard the term “database” thrown around, but may or may not have a clear idea what it means. Put simply, a database is any system designed to create, store, retrieve, and manage a large amount of digital information. There are many different kinds of databases, but the most common kind is a “relational database”, a database that uses multiple tables (and each table has many rows and columns) to store the necessary data. Most modern databases are technically a RDBMS, a “relational database management system”, which is a way of describing a database (and any attendant software) that uses the relational model.

The most popular and widely-used open-source RDBMS currently in use is a program called MySQL. Two computer programmers named Michael Widenius and David Axmark began developing MySQL in 1994, and the software was eventually acquired by Sun Corporation, and then by Oracle Corporation, when Oracle bought Sun in 2010\. The name “MySQL” comes from two sources. The “My” part apparently comes from Michael Widenius’s daughter, named My. The “SQL” comes from “Structured Query Language”, which is a computer language designed to handle the tasks of inserting, retrieving, managing, and deleting data in an RDBMS.

MySQL has been around for a long time, and it’s used in a lot of websites – Google, Facebook, and Wikipedia all use MySQL, and many of the more popular content management systems, like WordPress and Drupal, rely on MySQL to store data.

MySQL installs quite easily on a Linux Mint system. In this chapter, we’ll show you how to install and configure MySQL, how to create databases and database users from the MySQL command line, and how to install phpMyAdmin for an easier, graphical-based means of configuring MySQL

INSTALL MYSQL SERVER

To install MySQL Server on Linux Mint, make your way to a Terminal window or a command prompt, and type this command:

sudo apt-get install mysql-server-5.7

(As of this writing, MySQL Server version 5.7 is the latest version available in the Linux Mint repositories, though future versions of Linux Mint may receive the newer versions of MySQL.)

Enter your password to authenticate, and apt will download the MySQL files and install them for you. It’s a big set of files, so depending on the speed of your Internet connection, it might take a while to download. After the files are downloaded and are installing, the installer will ask you for a password for MySQL’s root user. Just as the root user in Linux has complete control over the system, the root user in MySQL has absolute control over all databases, tables, permissions, and users. For obvious security reasons, you’ll want to create an extremely strong password (a mixture of uppercase, lowercase, numbers, and punctuation, the longer the better) for your MySQL root user.

(Note that in the password dialog box, if you can’t get the <OK> field selected, you can use the tab key to jump from the text input line to the <OK> field.)

After you enter the root password, the installer will finish working with the MySQL files, and return you to the command line.

Next, you’ll want to run the mysql_secure_installation script to tighten up security on your new MySQL server. Run this command from the prompt:

sudo mysql_secure_installation

First, the mysql_secure_installation script will ask you to enter the current password for the MySQL root user. After you do that, it will ask if you want to change the root password. Since you already set a root password, you can hit “n” (unless you want to change it again for some reason).

Next, the script will ask you to setup the VALIDATE PASSWORD plugin, which checks passwords for appropriate strength. Hit Y to accept, and then set the password strength level by hitting 0 for Low, 1, for Medium, and 2 for Strong.

Next, the script will ask if you want to remove the anonymous user. The anonymous user, like anonymous access in FTP, lets someone log into MySQL without having a proper user account. For security reasons, it’s always best to remove the anonymous user, so hit “y” to continue.

After that, the script will ask if you want to prevent the MySQL root user from logging in remotely to the MySQL server. Always hit “y” to forbid root remote access, since if an attacker guesses your root password, he can destroy your databases or steal the information they contain.

After this, the script will ask if you want to remove the test database. MySQL includes a test database that anyone can access. Again, this is a security hole, so you’ll want to hit “y” to remove the test database.

The script will then ask to reload the privilege tables so the changes take effect. Hit “y”, and the **mysql_secure_installation** script will conclude and return you to the command line.

MySQL server is now installed on your Linux Mint system. In the next section, we’ll discuss using the MySQL command-line client to create databases and users.

USING THE MYSQL COMMAND-LINE CLIENT

The most common use for MySQL on a Linux Mint system is to provide a backend for a dynamic website of some kind, usually content management systems like WordPress or MediaWiki. To host these websites on a Linux Mint machine, you’ll need to create a database and a database user for the website. MySQL Server can support many different databases, limited by the amount of hardware and disk space available on the machine. (Hosting multiple active databases at the same time places a high level of demand upon a hard drive.)

Like Samba, MySQL has its own collection of user accounts, separate from the main system accounts, called "database users." A database user is simply a MySQL user that has access to a particular database, or specific tables within a database. In this section, we’ll show you how to create database and users with the command-line client.

First, you'll need to get to the MySQL client prompt. The MySQL command-line client, like the command-line clients for FTP and SFTP, has its own prompt. To access that prompt and start the client, use this command:

mysql

However, if you simply type the command, it will bounce back with an error message. To use the MySQL command-line client, you need to add the -u and the -p switches as well. The -u switch tells it what MySQL user you want to use to log into the client (similar to the -l switch with SSH). The -p switch tells it to ask for the password. So, to use the MySQL client as the MySQL root user, the command should look like this:

mysql -u root -p

Enter the password for the MySQL root user, and you'll find yourself at the MySQL command prompt, which will look like this:

mysql>

Our next steps are to create a database, create a user to access that database, and grant our new user all rights to that database. Generally, when you're installing a web application like WordPress, you'll give the database user you create for the WordPress application all rights to the WordPress database so it can function properly. Not giving the application user all rights to the database can cause the application to act erratically or even fail entirely (though some applications can work with limited access to its database).

An important note before we continue, though. All commands made from the MySQL prompt must end with a semicolon to denote the end of the statement. Any commands that do not end with a semicolon will not work. With that in mind, let's first create a database.

To create a database, use this command at the **mysql>** prompt:

CREATE DATABASE newdatabase;

The MySQL client will respond with a message that should say "Query OK, 1 row affect (0.00 sec)." This means the command was successful, and a new database named "newdatabase" has been created.

Next, you'll create a user who will access that database:

CREATE USER newdatabaseruser;

You should get the "Query OK" message again. Once the new user is created, we'll need to set a password for the user before we can assign any permissions. In this example, we'll assign a password of "1234". However, in real life, just as with the root user, you'll want to assign a strong password. (This database user won't have full control over the MySQL server as the root user does, but we will give it full control over the database we just created, and a malicious user who guesses the password could cause all kinds of trouble.) To create the password, use this command:

SET PASSWORD FOR newdatabaseuser= PASSWORD(“1234”);

Again you should get the "Query OK" confirmation message. The final step is to assign all privileges on the "newdatabase" database to the "newdatabaseuser" user. Use this command to assign the permissions:

GRANT ALL PRIVILEGES ON newdatabase.* TO newdatabaseuser IDENTIFIED BY ‘1234;

That isn't a typo - those are single quote marks (') instead of the usual double quote marks (") that were used in the command to set the password. MySQL's internal syntax, alas, isn't always consistent. Anyway, if you typed the command correctly, you should get the "Query OK" confirmation again.

Once you are done, use this command to quit the MySQL command-line interface:

exit

You've now set up a database, created a database user, and given that user full control over that database.

BACK UP AND RESTORE MYSQL DATABASES

MySQL databases are often used to power web applications such as WordPress or Moodle, which means that those MySQL databases often wind up holding vital information. Therefore, it is important to back them up on a regular basis. A quick and easy way to backup a MySQL database is with the mysqldump command-line tool. This tool downloads the database into a single SQL file, which you can store as a backup or use to transfer the database to another MySQL server.

To use mysqldump, you will need to know the root password of the MySQL server (or a user with permissions to the database you need to download).

In this example, we will dump a database named data into a file named data.sql:

**mysqldump -u root -p data > data.sql**

Enter the root password, and mysqldump will dump the database information into the data.sql file.

To transfer the database to a new server, first create a blank database on the server from the MySQL command prompt. In this example, this command will create a new database named datanew:

**CREATE DATABASE datanew;**

Then transfer the data.sql file to the new server and write it onto the new database with this command:

**mysql -u root -p datanew < data.sql**

The datanew database will receive all the tables and columns contained in the data.sql file. Note that this command completely overwrites the target database with the information in the SQL file, so make sure to select the correct database!

INSTALLING PHPMYADMIN

It is possible to administer MySQL Server entirely from its command line client.

But if you read through the previous section, you probably noticed that the MySQL command-line client is a lot of work, and rather cumbersome to boot. Remembering the syntax is something of a challenge, and occasionally even veteran database administrators have a hard time working through complex SQL statements. I am a big believer in doing as much as possible from the command line, but sometimes the GUI is in fact quicker and easier. MySQL administration is often one of those cases.

Fortunately, MySQL has a GUI available, a program called phpMyAdmin. It's a web interface, which means that you connect to it via a web browser from another computer. It runs off the PHP scripting language (which we'll discuss more in the next chapter), and lets you quickly and efficiently make changes to your MySQL Server. It even lets you enter command-line SQL statements, if you prefer.

Obviously, you will need MySQL Server installed before you can install phpMyAdmin. Once you have MySQL installed, you’re ready to begin.

To install phpMyAdmin, go to a Terminal window or command prompt and type this command:

**sudo apt-get install phpmyadmin**

This will download and install phpMyAdmin on your Linux Mint system. The phpMyAdmin package comes with quite a lot of dependencies, so the downloading and installation might take some time.

Once the package starts installing, it will ask you whether or not you want to use Apache or lighttpd for phpMyAdmin’s web server. Generally, unless you have a good reason to do otherwise, I’d recommend that you use Apache. (You can use the tab key to move the cursor while within the dialog box, if you get stuck.)

Next, the installer will ask if it can create and configure a database for phpMyAdmin using the dbconfig-common script. If you’re a first-time user, and don’t have advanced configuration needs, then use the tab key to select Yes and hit enter. The script will ask you for the password of your MySQL server’s root user. Enter the password, and the installer will continue.

The installer will then ask for a password for phpMyAdmin’s database user. Select a password for the database user. Remember, as always, to set a strong password, with a mixture of uppercase letters, lowercase letters, numerals, and punctuation. You'll then need to enter the password again.

After that, the installer will wrap up and return you to the command line. If you installed it locally, you can then access your new phpMyAdmin installation by opening up a web browser on your Linux Mint system and navigating to this address:

http://127.0.0.1/phpmyadmin

Enter your MySQL root user and password, and you’ll have access to phpMyAdmin.

You can also access phpMyAdmin from a remote computer. For instance, if you installed phpMyAdmin on the machine with the IP address of 192.168.1.100, you would access it with this address:

http://192.168.1.100/phpmyadmin

***

## Chapter 15 - Installing Web Applications (WordPress, MediaWiki, and Moodle)

Hosting web applications is where Linux really shines. As we mentioned in Chapter 11, Apache servers running on Linux or UNIX-like systems comprise around a third or so or so of the Internet. Linux Mint can run a variety of web applications, ranging from simple interactive sites to powerful content management systems.

A “content management system” is a web application that lets people publish content to a website without deep knowledge of HTML or PHP coding. In this chapter, we’ll discuss how to install three of the most popular content management systems on a Linux Mint web server – WordPress, MediaWiki, and Moodle. These three content management systems provide the backend for millions of websites across the Internet.

However, WordPress, MediaWiki, and Moodle are all powered by something called a LAMP server, which we’ll discuss in the next section.

THE LAMP SERVER

LAMP is simply an acronym for Linux, Apache, MySQL, and PHP (or Perl and Python). These four software components provide a powerful web server and the backend of content management systems like WordPress, MediaWiki, and Moodle. In a LAMP server, Linux is the operating system. Apache is the web server, and MySQL the database backend.

We’ve discussed both Apache and MySQL, but we haven’t yet mentioned the “P” in “LAMP” - PHP. PHP is a “scripting language”, which is a kind of computer language written specifically to control a particular software or hardware component. In this case, PHP was developed to control and manage dynamic web pages. (PHP originally stood for “Personal Home Page”, but now stands for “PHP: Hypertext Processor.”) WordPress, MediaWiki, and Moodle are all written to use PHP. In the next sections, we’ll discuss how to install WordPress, MediaWiki, and Moodle on a Linux Mint machine.

(If you read straight through the next few sections, you’ll notice that I’ll repeat a lot of the directions we already discussed. There are two reasons for that. The first is that WordPress, MediaWiki, and Moodle all use a lot of the same software components. The second is that I wanted each web app to have its own complete set of instructions, so I don’t have to say “next, install Apache like we discussed in Chapter 11”, which means you don’t have to scroll back and forth. I personally hate it when technical writers do that, so I’m not going to do that here. Besides, this is an ebook, so it’s not as if repeating some directions will drive up the printing costs.)

INSTALL WORDPRESS ON Linux Mint

WordPress, first developed in 2003, is a content management system that runs quite a variety of websites. In WordPress’s early days, it tended to run only personal blogs and smaller sites. However, the software improved considerably with every version, and it’s adaptable enough to be used for a variety of different sites. WordPress’s big break came in 2009 when popular blogging platform Movable Type made unpopular changes to its licensing terms. Enough Movable Type users were annoyed with the change to migrate to WordPress, and WordPress is the dominant open-source content management system on the Internet as of this writing.

It’s quite possible to install WordPress on a machine running either the desktop or the server version of Linux Mint. This makes an excellent environment for testing and experimentation, since you can tweak and experiment to your heart’s desire without rendering your production blog inoperable. If you need to run an internal corporate blog of some kind, hosting WordPress on an Linux Mint box or virtual machine is a cheaper solution than more expensive blogging or collaboration software. Or, if you’re really ambitious (and you can afford the bandwidth), you can host an Internet-accessible WordPress blog out of your apartment.

Let’s begin!

(Note that the Linux Mint repositories now contain a fully automated WordPress installation. However, I believe that installing it by hand yourself has significant value – you’ll not only learn how to set up a LAMP server, but installing step-by-step gives you valuable troubleshooting knowledge later on in case something breaks.)

First, install Linux Mint into your machine of choice. Once Linux Mint is installed and updated, you will need to install five pieces of software: the Apache web server, the MySQL database server version 5.7, PHP version 7, the MySQL module for PHP, and finally the WordPress software itself.

First, install the Apache web server. To install Apache, go to a Terminal window or a command prompt and type this command:

sudo apt-get install apache2

(Technically, you’ll be installing Apache 2, the latest version.)

Enter your password to authenticate, follow the default prompts, and apt will download and install the Apache web server for you.

And that’s it! Apache should now be working. To test it from the web server itself, go to a web browser and visit the address http://127.0.0.1\. You’ll remember that this is the “local loopback” address, basically the address the computer uses to refer to itself. Alternatively, you could test it from another computer on the same subnet. For instance, if you installed Apache on a computer with an IP address of 192.168.1.100, you could test it by going to another computer on the same subnet and visiting http://192.168.100 from the web browser.

Regardless, if Apache is working properly, you should see the default Apache/Linux Mint web page with the Linux Mint logo in the upper left-hand corner.

Apache is now operational.

The next step to install WordPress is to install the MySQL database server. Return to the Terminal and type this command:

sudo apt-get install mysql-server-5.7

(As of this writing, MySQL Server version 5.7 is the latest version available in the Linux Mint repositories, though future versions of Linux Mint may receive the newer versions of MySQL.)

Enter your password to authenticate, and apt will download the MySQL files and install them for you. It’s a big set of files, so depending on the speed of your Internet connection, it might take a while to download. After the files are downloaded and are installing, the installer will ask you for a password for MySQL’s root user. Just as the root user in Linux has complete control over the system, the root user in MySQL has absolute control over all databases, tables, permissions, and users. For obvious security reasons, you’ll want to create an extremely strong password (a mixture of uppercase, lowercase, numbers, and punctuation, the longer the better) for your MySQL root user.

(Note that in the password dialog box, if you can’t get the <OK> field selected, you can use the tab key to jump from the text input line to the <OK> field.)

After you enter the root password, the installer will finish working with the MySQL files, and return you to the command line.

Next, you’ll want to run the mysql_secure_installation script to tighten up security on your new MySQL server. Run this command from the prompt:

sudo mysql_secure_installation

First, the mysql_secure_installation script will ask you to enter the current password for the MySQL root user. After you do that, it will ask if you want to change the root password. Since you already set a root password, you can hit “n” (unless you want to change it again for some reason).

Next, the script will ask you to setup the VALIDATE PASSWORD plugin, which checks passwords for appropriate strength. Hit Y to accept, and then set the password strength level by hitting 0 for Low, 1, for Medium, and 2 for Strong.

Next, the script will ask if you want to remove the anonymous user. The anonymous user, like anonymous access in FTP, lets someone log into MySQL without having a proper user account. For security reasons, it’s always best to remove the anonymous user, so hit “y” to continue.

After that, the script will ask if you want to prevent the MySQL root user from logging in remotely to the MySQL server. Always hit “y” to forbid root remote access, since if an attacker guesses your root password, he can destroy your databases or steal the information they contain.

After this, the script will ask if you want to remove the test database. MySQL includes a test database that anyone can access. Again, this is a security hole, so you’ll want to hit “y” to remove the test database.

The script will then ask to reload the privilege tables so the changes take effect. Hit “y”, and the **mysql_secure_installation** script will conclude and return you to the command line.

MySQL server is now installed on your Linux Mint system.

The next step to installing WordPress is to install PHP version 7:

sudo apt-get install php

Next, install the libapache2-mod-php7.0 library, which allows PHP to communicate properly with Apace:

sudo apt-get install libapache2-mod-php7.0

Then install the MySQL module for PHP:

sudo apt-get install php-mysql

You may also want to install the GD library for PHP, since many WordPress plugins rely on it for graphical manipulation (note that this is an optional step):

sudo apt-get install php-gd

Finally, download the WordPress software to your computer. You can obtain it from this address:

http://wordpress.org/latest.tar.gz

If you’re working exclusively from the command line, you can use this command to download the WordPress software:

wget http://wordpress.org/latest.tar.gz

Use this command to unpack the WordPress files:

tar -xzvf latest.tar.gz

Move the WordPress files over to the /var/www/html directory. (In this command, I’ll assume you unpacked the WordPress files to your home directory; you will have to adjust the command if you unpacked them in a different directory.)

sudo cp -r ~/wordpress/* /var/www/html/

Now that we’ve got our software installed and downloaded, we’ll need to configure it. First, we’ll need to prepare MySQL for use with WordPress. WordPress requires a database and a database user, and full permission for its database user to access its database. To start the MySQL command-line client, use this command:

mysql -u root -p

Enter the password for the MySQL root user, and you'll find yourself at the MySQL command prompt, which will look like this:

mysql>

Our next steps are to create a WordPress database, create a user to access that database, and grant our new user all rights to the WordPress database.

(An important note before we continue, though. All commands made from the MySQL prompt must end with a semicolon to denote the end of the statement. Any commands that do not end with a semicolon will not work. With that in mind, let's first create a database.)

To create a database for WordPress, use this command at the **mysql>** prompt:

CREATE DATABASE wordpress;

The MySQL client will respond with a message that should say "Query OK, 1 row affect (0.00 sec)." This means the command was successful, and a new database named "newdatabase" has been created.

Next, you'll create a user who will access that database and assign a password to that user. In this example, we'll assign a password of "1234". However, in real life, just as with the root user, you'll want to assign a strong password. (This database user won't have full control over the MySQL user as the root user does, but we will give it full control over the database we just created, and a malicious user who guesses the password could cause all kinds of trouble.):

CREATE USER wordpressuser IDENTIFIED BY '1234';

You should get the "Query OK" message again. The final step is to assign all privileges on the "wordpress" database to the "wordpressuser" user. Use this command to assign the permissions:

GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser IDENTIFIED BY ‘1234';

That isn't a typo - those are single quote marks (') instead of the usual double quote marks (") that were used in the command to set the password. MySQL's internal syntax, alas, isn't always consistent. Anyway, if you typed the command correctly, you should get the "Query OK" confirmation again.

Once you are done, use this command to quit the MySQL command-line interface:

exit

Now that we have MySQL prepared, we can now configure WordPress itself. Specifically, we’ll have to configure WordPress to talk to the database we just created. To do so, you must create a wp-config.php file in the WordPress directory. Fortunately, WordPress includes a handy wp-config-sample.php you can use as a template.

Type this command to create a wp-config file (assuming you installed WordPress in the /var/www/html directory):

sudo cp /var/www/html/wordpress/wp-config-sample.php /var/www/html/wp-config.php

Next, use vi to edit the newly created wp-config file:

sudo vi /var/www/html/wp-config.php

You’ll see that the wp-config.php file contains a number of variables. Change the following three variables:

-Change **putyourdbnamehere** to **wordpress** .

-Change **usernamehere** to **wordpressuser** .

-Change **yourpassword** here to **1234** .

Once you have your changes made (after double-checking the spelling, of course), switch vi to Command mode, and save your changed file.

Once is this is done, rename Apache's default index.html file to index.html.old. Otherwise Apache will access the default sample page instead of starting Wordpress:

sudo mv index.html index.html.old

Everything should now be ready. Open up a web browser, and navigate to http://127.0.0.1/. (If you want to access it from a different machine, of course, use the IP address of the WordPress server, for instance – http://192.168.1.100.) If you configured everything correctly, you should then be greeted by the WordPress configuration page. You’ll pick a username, and WordPress will assign you a password. Follow the prompts, and you will have a functional WordPress blog installed on a Linux Mint machine. Congratulations!

One final note: if you configure your blog from a local browser, it will probably set your blog’s address as http://127.0.0.1\. This is fine if you only want to view it from the host machine, but if you want to view it over the network, you’ll need to change it. Fortunately, you can do so quickly by going Options in the WordPress admin interface, and then to General, and changing the blog’s URL.

INSTALLING MEDIAWIKI ON Linux Mint

Wikipedia, that encyclopedia of a thousand “citations needed”, runs on an open-source web application called MediaWiki. A wiki, if you haven’t heard the term before, is basically an online encyclopedia that relies on user contributions. Wikis can range from broad, general-topic encyclopedias like Wikipedia itself, or devoted to a single topic, like a television show or a computer game. You can quite easily install MediaWiki and host your own wiki off a Linux Mint system. Installing MediaWiki on Linux Mint takes three steps: first, you install the prerequisite software packages, second, you configure the prerequisites, and third, you install MediaWiki and run its configuration script.

Let’s begin!

First, install Linux Mint into your machine of choice. Once Linux Mint is installed and updated, you will need to install five pieces of software: the Apache web server, the MySQL database server version 5.7, PHP version 7, the MySQL module for PHP, and finally the MediaWiki software itself.

First, install the Apache web server. To install Apache, go to a Terminal window or a command prompt and type this command:

sudo apt-get install apache2

(Technically, you’ll be installing Apache 2, the latest version.)

Enter your password to authenticate, follow the default prompts, and apt will download and install the Apache web server for you.

And that’s it! Apache should now be working. To test it from the web server itself, go to a web browser and visit the address http://127.0.0.1\. You’ll remember that this is the “local loopback” address, basically the address the computer uses to refer to itself. Alternatively, you could test it from another computer on the same subnet. For instance, if you installed Apache on a computer with an IP address of 192.168.1.100, you could test it by going to another computer on the same subnet and visiting http://192.168.100 from the web browser.

Regardless, if Apache is working properly, you should see the default Apache/Linux Mint web page with the Linux Mint logo in the upper left-hand corner.

Apache is now operational.

The next step to install MediaWiki is to install the MySQL database server. Return to the Terminal and type this command:

sudo apt-get install mysql-server-5.7

(As of this writing, MySQL Server version 5.7 is the latest version available in the Linux Mint repositories, though future versions of Linux Mint may receive the newer versions of MySQL.)

Enter your password to authenticate, and apt will download the MySQL files and install them for you. It’s a big set of files, so depending on the speed of your Internet connection, it might take a while to download. After the files are downloaded and are installing, the installer will ask you for a password for MySQL’s root user. Just as the root user in Linux has complete control over the system, the root user in MySQL has absolute control over all databases, tables, permissions, and users. For obvious security reasons, you’ll want to create an extremely strong password (a mixture of uppercase, lowercase, numbers, and punctuation, the longer the better) for your MySQL root user.

(Note that in the password dialog box, if you can’t get the <OK> field selected, you can use the tab key to jump from the text input line to the <OK> field.)

After you enter the root password, the installer will finish working with the MySQL files, and return you to the command line.

Next, you’ll want to run the mysql_secure_installation script to tighten up security on your new MySQL server. Run this command from the prompt:

sudo mysql_secure_installation

First, the mysql_secure_installation script will ask you to enter the current password for the MySQL root user. After you do that, it will ask if you want to change the root password. Since you already set a root password, you can hit “n” (unless you want to change it again for some reason).

Next, the script will ask you to setup the VALIDATE PASSWORD plugin, which checks passwords for appropriate strength. Hit Y to accept, and then set the password strength level by hitting 0 for Low, 1, for Medium, and 2 for Strong.

Next, the script will ask if you want to remove the anonymous user. The anonymous user, like anonymous access in FTP, lets someone log into MySQL without having a proper user account. For security reasons, it’s always best to remove the anonymous user, so hit “y” to continue.

After that, the script will ask if you want to prevent the MySQL root user from logging in remotely to the MySQL server. Always hit “y” to forbid root remote access, since if an attacker guesses your root password, he can destroy your databases or steal the information they contain.

After this, the script will ask if you want to remove the test database. MySQL includes a test database that anyone can access. Again, this is a security hole, so you’ll want to hit “y” to remove the test database.

The script will then ask to reload the privilege tables so the changes take effect. Hit “y”, and the **mysql_secure_installation** script will conclude and return you to the command line.

MySQL server is now installed on your Linux Mint system.

The next step to installing MediaWiki is to install PHP version 7:

sudo apt-get install php

Then install the MySQL module for PHP:

sudo apt-get install php-mysql

Then install the MySQL module for PHP:

sudo apt-get install php-mysql

Then install the mbstring PHP module:

sudo apt-get install php-mbstring

Then install the xml PHP module:

sudo apt-get install php-xml

Next, restart Apache with this command so that it reloads with all the PHP extensions enabled:

sudo /etc/init.d/apache2 restart

Finally, download the MediaWiki software to your Desktop. You can obtain it from this address:

https://www.mediawiki.org/wiki/Download

If you’re working exclusively from the command line, you can use this command to download the MediaWiki software:

wget https://releases.wikimedia.org/mediawiki/1.27/mediawiki-1.28.2.tar.gz

(Note that the version number, and hence the file name, WILL change with future versions of MediaWiki, so double-check before downloading the file.)

Use this command to unpack the MediaWiki files:

tar -xzvf mediawiki-1.27.1.tar.gz

Finally, move the MediaWiki files over to the /var/www/html directory. (In this command, I’ll assume you unpacked the MediaWiki files to your home directory; you will have to adjust the command if you unpacked them in a different directory.)

sudo cp -r ~/mediawiki-1.27.1/* /var/www/html

Now we’ll need to prepare MySQL for use with MediaWiki. MediaWiki requires a database and a database user, and full permission for its database user to access its database. To start the MySQL command-line client, use this command:

mysql -u root -p

Enter the password for the MySQL root user, and you'll find yourself at the MySQL command prompt, which will look like this:

mysql>

Our next steps are to create a MediaWiki database, create a user to access that database, and grant our new user all rights to the MediaWiki database.

(An important note before we continue, though. All commands made from the MySQL prompt must end with a semicolon to denote the end of the statement. Any commands that do not end with a semicolon will not work. With that in mind, let's first create a database.)

To create a database fmedor MediaWiki, use this command at the **mysql>** prompt:

CREATE DATABASE mediawiki;

The MySQL client will respond with a message that should say "Query OK, 1 row affect (0.00 sec)." This means the command was successful, and a new database named "newdatabase" has been created.

Next, you'll create a user who will access that database and assign a password to that user. In this example, we'll assign a password of "1234". However, in real life, just as with the root user, you'll want to assign a strong password. (This database user won't have full control over the MySQL user as the root user does, but we will give it full control over the database we just created, and a malicious user who guesses the password could cause all kinds of trouble.):

CREATE USER mediawikiuser IDENTIFIED BY '1234';

Again you should get the "Query OK" confirmation message. The final step is to assign all privileges on the "mediawiki" database to the "mediawikiuser" user. Use this command to assign the permissions:

GRANT ALL PRIVILEGES ON mediawiki.* TO mediawikiuser IDENTIFIED BY ‘1234';

That isn't a typo - those are single quote marks (') instead of the usual double quote marks (") that were used in the command to set the password. MySQL's internal syntax, alas, isn't always consistent. Anyway, if you typed the command correctly, you should get the "Query OK" confirmation again.

Once you are done, use this command to quit the MySQL command-line interface:

exit

Once is this is done, rename Apache's default index.html file to index.html.old. Otherwise Apache will access the default sample page instead of starting Wordpress:

sudo mv index.html index.html.old

Once the permissions have been set, launch the installation script by navigating here in your Linux Mint system’s web browser:

http://127.0.0.1

The installation script is simply a web form you’ll need to fill out. The default settings will work for the most part. You’ll need to pick a name for your wiki, and you’ll also need to enter the database name, the database user, and the password you created for MySQL. You will also need to set an administrator username and password for the wiki. Once you have appropriate information entered, complete the script, and MediaWiki will be installed.

However, you’ll need to do one more thing to finish the installation. After you complete the install script, MediaWiki will generate a LocalSettings.php file and offer it to you for download. Make sure to download the file and then transfer it to the /var/www/html file in order to complete the installation. (You may need to use SSH and SFTP to do this - see Chapter 10 on how to set them up.)

MediaWiki should now be functioning on your Linux Mint system.

INSTALLING MOODLE ON Linux Mint

Moodle is a virtual learning environment used by tens of thousands of schools across the world. Using Moodle, you can create a fully online course, or use it to supplment a traditionally-taught classroom course. Best of all, Moodle is free, and you can install it on Linux Mint. Installing Moodle on Linux Mint is a bit of work, but once it is finished, you’ll have a robust e-learning server application.

It’s quite possible to install Moodle on a machine running either the desktop or the server version of Linux Mint. This makes an excellent environment for testing and experimentation, since you can tweak and experiment to your heart’s desire without rendering your production site inoperable. Given that Moodle is free, if you have a bit of Linux knowledge, you can use Moodle in lieu of far more expensive alternatives.

Let’s begin!

First, install Linux Mint into your machine of choice. Once Linux Mint is installed and updated, you will need to install five pieces of software: the Apache web server, the MySQL database server version 5.7, PHP version 7, the MySQL module for PHP, and finally the WordPress software itself.

First, install the Apache web server. To install Apache, go to a Terminal window or a command prompt and type this command:

sudo apt-get install apache2

(Technically, you’ll be installing Apache 2, the latest version.)

Enter your password to authenticate, follow the default prompts, and apt will download and install the Apache web server for you.

And that’s it! Apache should now be working. To test it from the web server itself, go to a web browser and visit the address http://127.0.0.1\. You’ll remember that this is the “local loopback” address, basically the address the computer uses to refer to itself. Alternatively, you could test it from another computer on the same subnet. For instance, if you installed Apache on a computer with an IP address of 192.168.1.100, you could test it by going to another computer on the same subnet and visiting http://192.168.100 from the web browser.

Regardless, if Apache is working properly, you should see the default Apache/Linux Mint web page with the Linux Mint logo in the upper left-hand corner.

Apache is now operational.

The next step to install WordPress is to install the MySQL database server. Return to the Terminal and type this command:

sudo apt-get install mysql-server-5.7

(As of this writing, MySQL Server version 5.7 is the latest version available in the Linux Mint repositories, though future versions of Linux Mint may receive the newer versions of MySQL.)

Enter your password to authenticate, and apt will download the MySQL files and install them for you. It’s a big set of files, so depending on the speed of your Internet connection, it might take a while to download. After the files are downloaded and are installing, the installer will ask you for a password for MySQL’s root user. Just as the root user in Linux has complete control over the system, the root user in MySQL has absolute control over all databases, tables, permissions, and users. For obvious security reasons, you’ll want to create an extremely strong password (a mixture of uppercase, lowercase, numbers, and punctuation, the longer the better) for your MySQL root user.

(Note that in the password dialog box, if you can’t get the <OK> field selected, you can use the tab key to jump from the text input line to the <OK> field.)

After you enter the root password, the installer will finish working with the MySQL files, and return you to the command line.

Next, you’ll want to run the mysql_secure_installation script to tighten up security on your new MySQL server. Run this command from the prompt:

sudo mysql_secure_installation

First, the mysql_secure_installation script will ask you to enter the current password for the MySQL root user. After you do that, it will ask if you want to change the root password. Since you already set a root password, you can hit “n” (unless you want to change it again for some reason).

Next, the script will ask you to setup the VALIDATE PASSWORD plugin, which checks passwords for appropriate strength. Hit Y to accept, and then set the password strength level by hitting 0 for Low, 1, for Medium, and 2 for Strong.

Next, the script will ask if you want to remove the anonymous user. The anonymous user, like anonymous access in FTP, lets someone log into MySQL without having a proper user account. For security reasons, it’s always best to remove the anonymous user, so hit “y” to continue.

After that, the script will ask if you want to prevent the MySQL root user from logging in remotely to the MySQL server. Always hit “y” to forbid root remote access, since if an attacker guesses your root password, he can destroy your databases or steal the information they contain.

After this, the script will ask if you want to remove the test database. MySQL includes a test database that anyone can access. Again, this is a security hole, so you’ll want to hit “y” to remove the test database.

The script will then ask to reload the privilege tables so the changes take effect. Hit “y”, and the **mysql_secure_installation** script will conclude and return you to the command line.

MySQL server is now installed on your Linux Mint system.

Now we’ll need to prepare MySQL for use with Moodle. Moodle requires a database and a database user, and full permission for its database user to access its database. To start the MySQL command-line client, use this command:

mysql -u root -p

Enter the password for the MySQL root user, and you’ll find yourself at the MySQL command prompt, which will look like this:

mysql>

Our next steps are to create a Moodle database, create a user to access that database, and grant our new user all rights to the Moodle database.

(An important note before we continue, though. All commands made from the MySQL prompt must end with a semicolon to denote the end of the statement. Any commands that do not end with a semicolon will not work. With that in mind, let’s first create a database.)

To create a database for Moodle, use this command at the mysql> prompt:

CREATE DATABASE moodle;

The MySQL client will respond with a message that should say “Query OK, 1 row affect (0.00 sec).” This means the command was successful, and a new database named “newdatabase” has been created.

Next, you'll create a user who will access that database and assign a password to that user. In this example, we'll assign a password of "1234". However, in real life, just as with the root user, you'll want to assign a strong password. (This database user won't have full control over the MySQL user as the root user does, but we will give it full control over the database we just created, and a malicious user who guesses the password could cause all kinds of trouble.):

**CREATE USER moodleuser IDENTIFIED BY '1234';**

Again you should get the "Query OK" confirmation message. The final step is to assign all privileges on the “moodle” database to the “moodleuser” user. Use this command to assign the permissions:

GRANT ALL PRIVILEGES ON moodle.* TO moodleuser IDENTIFIED BY ‘1234′;

That isn’t a typo – those are single quote marks (‘) instead of the usual double quote marks (“) that were used in the command to set the password. MySQL’s internal syntax, alas, isn’t always consistent. Anyway, if you typed the command correctly, you should get the “Query OK” confirmation again.

Once you are done, use this command to quit the MySQL command-line interface:

exit

The next step to installing Moodle is to install PHP version 5, along with the necessary PHP modules. First, install PHP 5 with this command:

sudo apt-get install php

Next, install the libapache2-mod-php7.0 library, which allows PHP to communicate properly with Apace:

sudo apt-get install libapache2-mod-php7.0

After this, you will need to install several different PHP extensions not included with the default PHP 5 implementation on Linux Mint. First, install the MySQL module for PHP:

sudo apt-get install php-mysql

You must also install the GD library for PHP:

sudo apt-get install php-gd

The JSON extension is also required:

sudo apt-get install php-json

The CURL extension:

sudo apt-get install php-curl

The XML extension:

sudo-apt-get install php-xml

The XMLRPC extension:

sudo apt-get install php-xmlrpc

The ZIP extension:

sudo apt-get install php-zip

The MBSTRING extension:

sudo apt-get install php-mbstring

The SOAP extension:

sudo apt-get install php-soap

And, finally, the INTL extension:

sudo apt-get install php-intl

After all the plugins have installed, restart Apache so it recognizes the plugins properly:

sudo /etc/init.d/apache2 restart

Finally, download the Moodle software to your Desktop. You can obtain it from this address:

http://download.moodle.org

Move the Moodle files over to the /var/www/html directory. (In this command, I’ll assume you unpacked the moodle files to your home directory; you will have to adjust the command if you unpacked them in a different directory.)

sudo cp -r ~/moodle/* /var/www/html

After that, rename the old index.html file in /var/www so Apache uses Moodle’s PHP files for the site, not the index.html file:

sudo mv index.html index.html.old

Now that we’ve got our software downloaded, we’ll need to configure it.

You will need to create a location for Moodle to save data files. Traditionally, the location is in /var/moodledata. (Creating the data directory inside the web server directory is an extremely bad idea, due to the resultant security holes.) To create the data directory, use this command:

sudo mkdir /var/moodledata

Use this command to change the owner of the directory to the Apache system user. In Linux Mint, the Apache system user is usually named www-data:

sudo chown www-data /var/moodledata

Then use this command to make the /var/moodledata directory writable to Moodle:

sudo chmod -R 744 /var/moodledata

Now that configuration and setup is complete, we are actually read to begin installing Moodle!

Fire up a web browser and navigate to the Moodle location to launch the web-based installer. If your server’s IP address (for example) is 192.168.1.100, the address would look like this:

http://192.168.1.100

This will take you to the Moodle setup page.

First, select the language for your Moodle installation, and then click the Next button.

The installer will then ask for the locations of Moodle’s directories. The defaults will work, especially if you already created the /var/moodledata directory as indicated above. Click the Next button to continue.

Moodle will then ask what kind of database server to use. Since we already set up our MySQL database, select “Improved MySQL” and then hit the Next button.

Then installer will then need you to input the information for the database and database user we created above. Since our MySQL server is on the same machine as Moodle, leave “localhost” for the Database Host field. Enter “moodle” for Database Name, “moodleuser” for Database User, and then ’1234′ for Database Password. Leave the other fields blank, and then click Next.

Moodle will then generate a config.php file. Copy and paste the data of the config.php file, save it as “config.php”, and then transfer it to your server. Make sure to put it in the directory containing the Moodle installation – in this example, /var/www. Once the config.php is in place, make sure to mark it as executable with this command, otherwise the installation will halt:

sudo chmod 744 /var/www/html/config.php

Save config.php file, and then go back to the web browser and click the Next button.

Moodle will then ask if you agree to the terms of service. If you do, click the Continue button.

The installer will then run a system check to make sure your server has all the necessary software to support Moodle. If not (it’s common to forget one of the PHP extensions), the installation will pause to allow you to install the missing software. Once you have, click Reload. If all the checks are passed, you can click the Continue button to continue.

The Moodle installer will then start building the database tables it requires in the database we created earlier. The Moodle database is large and complex, and building the database may take a considerable amount of time, so be patient. As the installer successfully builds database tables, they will scroll down in the browser window. Once the database construction is complete, the Continue button will appear at the very bottom of the page. Click on it to continue.

Moodle will then display a form for you to set up an administrator account for your new site. Enter an appropriate username and a strong password, along with any other required fields. Once you have finished, click on the Update Profile button at the bottom of the page.

The install will then ask you to pick a full site name and a short name for the site. Select suitable names, and then click the Save Changes button.

Congratulations! Your Moodle installation is now complete, and you can begin adding courses and other materials. For additional documentation, the Moodle site contains many useful resources:

[http://docs.moodle.org/26/en/Main_page](http://docs.moodle.org/26/en/Main_page)

***

## Chapter 16 - The Six Best Applications for a New Linux Mint Desktop Installation

We’ve been looking at how to set up Linux Mint as a server platform, but in this chapter we’re going to shift gears and look at some of the best applications available for the Linux Mint desktop.

One of Linux Mint’s big advantages over Microsoft Windows is the large number of applications included with a standard Linux Mint software install. With Microsoft Windows, you get a few games, a few utilities, and WordPad, which doesn’t even include spell check. Linux Mint, on the other hand, comes with a wealth of preinstalled software. It includes LibreOffice, a full-featured free software suite. It comes with a variety of games, sound & video tools, utilities, productivity applications, and others. In fact, many users don’t need to install additional software, simply because the applications included with Linux Mint are adequate to their needs.

However, there are a lot of excellent applications that are not included with the Linux Mint install disc. In this chapter, we’re going to look at six of the best applications for Linux Mint, and how to install them.

VLC MEDIA PLAYER

VLC Media Player is a handy program that can play numerous forms of video, and runs on just about any OS platform. It also runs on Linux Mint, and installing it is quite simple.

First, open up a Terminal window and type this command:

sudo apt-get install vlc

Enter your password to authenticate, and apt will download and install VLC and its various dependencies for you. (You can also install it through Synaptic Package Manager and Linux Mint Software Center.) Afterwards you can launch VLC by going to the mintmenu, searching for "VLC", and clicking on the VLC icon.

VIRTUALBOX OSE

Virtualization is an extremely useful software concept. If you’re unfamiliar with the term, a “virtual machine” is a software process on a computer that mimics a separate, running computer. So, let’s say you have a computer with Linux Mint and install some sort of virtualization software on it. You can then create virtual machines – one running say, Windows XP, another running Windows 7, and perhaps still another running Fedora Linux.

I have found virtualization to be incredibly useful in my work. In the old days, if you wanted to test an application or program, you had to install it on your primary machine, to dig up an old machine to test it – and that meant another monitor and keyboard and all the other attendant clutter on your desk. With virtualization, you can have a second OS running as a window your main machine.

There are a number of virtualization products available for Linux Mint, but in my opinion, Virtualbox OSE offers the best balance between ease of use and features. To install Virtualbox, simply go to a Terminal window and type this command:

sudo apt-get install virtualbox

And that’s it! The apt utility will download Virtualbox and its dependencies, and then will then automatically execute its rather lengthy installation script. As ease of installation goes, you can’t beat that. After the installation is finished, you can start Virtualbox by going to the mintmenu, searching for "virtualbox", and clicking on the Virtualbox OSE icon.

Covering virtualization in depth is way beyond the scope of this book – entire books can (and have) been written about virtualization. But I urge you to experiment with it, as it is a superb and low-cost way of teaching yourself additional skills.

GOOGLE CHROME

The desktop edition of Linux Mint comes with the excellent Mozilla Firefox browser. However, Google’s Chrome browser, released in late 2008, has gained a powerful following. Google makes Chrome available for a variety of platforms, and Linux Mint is no exception.

To install Chrome on Linux Mint, first visit the Google Chrome website:

http://www.google.com/chrome

Click on the Download button, which will take you to the download page. Select the 64-bit version for Linux Mint. Hit the accept and install button, and the Chrome installer will download.

Once the download is complete, you’ll have a *.deb installer package for Chrome in your Downloads folder. Double-click on it to launch the installer. You’ll be taken to the Linux Mint Software application. Click on the Install button to begin the installation of Chrome.

You’ll need to enter your password to authenticate, and then follow the default prompts to install Chrome.

After the installation is complete, you can launch Chrome by clicking on the mintmenu, searching for Chrome, and clicking on the Chrome icon.

AUDACITY

Another application Linux Mint lacks is an editor for digital audio. Which admittedly makes sense, as not that many people need to edit digital audio on a regular basis. If you do need to edit audio files, however, the Audacity application is excellent. And it’s also available for Linux Mint.

To install Audacity, make your way to the Terminal window and type this command:

sudo apt-get install audacity

This will download and install Audacity and its dependencies from the Linux Mint repositories. Once finished, you can run Audacity by going to the mintmenu, searching for "audacity", and clicking on the Audacity icon.

However, the default install of Audacity lacks the ability to export its projects as an MP3 file. To gain that functionality, you’ll need to install the LAME library, which gives Audacity the ability to encode MP3 files. Note that the ownership of the MP3 patents remain in some dispute, so there may be liability issues in using LAME. However, if you’re in the legal clear, you can use this Terminal command to install the LAME library:

sudo apt-get install libmp3lame0

This will gave Audacity the ability to export projects as MP3 files.

DROPBOX

Dropbox is a useful file-sharing and syncing service that lets you sync files between different machines over the Internet for free. It’s very useful for backing up your important documents, pictures, MP3 files, video files, and other data. A Dropbox client that integrates with the Nautilus file manager is available for Linux Mint, and it’s quite simple to install. Here’s how to do it.

First, launch a new Terminal window by searching for Terminal in the mintmenu, or by hitting the CTRL+ALT+T keys simultaneously. Once the Terminal launches, type this command at the prompt:

**sudo apt-get install nautilus-dropbox** 

Enter this command, and then enter your password to authenticate. The apt-get utility will then download and install the Dropbox client for you.

Once the installation is complete, go to the mintmenu again, search for “Dropbox”, and click on the Dropbox icon. The Dropbox application will launch, and will ask you to download Dropbox’s proprietary Linux daemon. You will need to download the daemon to use Dropbox, so go ahead and allow the installation.

Once it is finished, Dropbox will launch. Enter your Dropbox credentials, and you can start using Dropbox with Linux Mint.

FILEZILLA

Linux Mint comes with both built-in command line SFTP and FTP clients, but if you find yourself working with file uploads a great deal, you might prefer to switch to a graphical FTP client for ease of use. Fortunately, the popular FileZilla FTP client is available for Linux Mint, and it's easy to install.

First, launch a new Terminal window by searching for Terminal in the mintmenu, or by hitting the CTRL+ALT+T keys simultaneously. Once the Terminal launches, type this command at the prompt:

sudo apt-get install filezilla

Enter this command, and then enter your password to authenticate. The apt-get utility will then download and install the FileZilla FTP client for you.

Once the installation is complete, go to the mintmenu again, search for “FileZilla”, and click on the FileZilla icon. Once the application launches, you can create a new connection by going to the File menu, selecting Site Manager, and entering the information for the site to which you wish to connect.

***

## Chapter 17 - Gaming

So far in this book we’ve talked a lot about the command line, server applications, and desktop productivity applications, but you can also have fun with your computer. (Though installing Samba, of course, is its own special kind of fun!) There is a wealth of computer game software available for Linux Mint, and in this chapter I’ll discuss some of my favorites.

However, we must first make an uncomfortable admission. The gaming experience on Linux Mint is generally not as good as the gaming experience on a Microsoft Windows machine, a mobile device like an iPad or iPhone or a Kindle Fire, and a dedicated game console like an XBox or a Playstation. This is because while Linux dominates in the server room, it retains only a tiny desktop usage share, and consequently major game publishers tend to release their games only for Windows machines, mobile devices, and game consoles. (In fact, it tends to cause something of a stir when a game publisher releases a title for both Windows *and* Mac OS X.) It is possible to get major Windows games to play on Linux Mint using Wine, but it’s a lot of work and not always reliable (we’ll discuss that more in the next chapter).

That said, in the six years since the first edition of this book was published, the situation has changed quite a bit. The biggest platform for gaming, Steam, now works on Linux Mint, and many games have been made available for Linux Mint. Another popular game store, GOG.com, offers many classic DOS games for Linux Mint via the DOSBox utility, and even a few newer games like Pillars Of Eternity or FTL: Faster Than Light.

Because of the changes over the last few years, there are quite a few enjoyable native games for Linux Mint. We’ll discuss a few of the classic ones here. And while playing modern Windows games on a Linux Mint system is a challenge, playing old DOS game is a breeze, ironically enough – we’ll show you how to do that as well.

CHESS

Mac OS X and some editions of Windows 7 used to come with a chess game, but Linux Mint does not. Linux Mint does come with the usual assortment of free games – Solitaire, a tile game, some word puzzles – but no chess games. Fortunately, restoring Linux Mint to chess parity with Mac OS X and Windows 7 is quite easy. There is a package of free software called GNOME Games, and it includes a chess game. And as the GNOME Games package is native to Linux, it’s quite easy to install on Linux Mint.

Simply go to the Terminal and type this command:

sudo apt-get install gnome-games

Enter your password to authenticate, and apt will download and install the missing GNOME Games. After the installation is complete, you can find Chess by clicking on the mintmenu and searching for "Chess." You also get close to a dozen other free games with the GNOME Games pack; my favorite is Quadrapassel, a clone of the venerable Tetris puzzle game.

THE BATTLE FOR WESNOTH

In turn-based strategy games, you assemble resources, build armies, and lead your troops in battle against your opponents. In fantasy-turn based games, you do all that, but you can also use magical fireballs and lightning bolts to smite your opponents, and also raise magical creatures like dragons and elves to fill the ranks of your armies.

“The Battle For Wesnoth” is a free turn-based strategy game available for Windows, Mac, and almost all Linux platforms. A volunteer-supported project, the game has been around since 2003\. I’ve played it from time to time since 2006 or so, and “Wesnoth” has improved immensely in that time. The current incarnation of “The Battle For Wesnoth” is smooth, polished, and quite enjoyable to play.

And best of all, “Wesnoth” is both free and simple to install on Linux Mint. To install “Wesnoth”, simply go to a Terminal prompt and type this command:

sudo apt-get install wesnoth

Put in your password to authenticate, and apt will download and install Wesnoth. The combined files are about 500 megabytes in size, so it might take some time. After the installation is complete, you can launch “Battle” by going to the mintmenu, searching for "Wesnoth", and clicking on the Battle for Wesnoth icon.

ANGBAND

Those of you who have been playing computer games long enough might remember the old Rogue style computer games. The Rogue games originated in 1980 with the original Rogue game, written to be played on university UNIX computer terminals. In Rogue, the player took the role of an adventurer descending ever deeper into an elaborate dungeon, slaying monsters, avoiding traps, and collecting gold and experience. (This, of course, remains a staple of computer gaming to this day.) The “Roguelike” games descended from the original Rogue game, improving on its ideas and execution, and many graphical games run off the original principles of Rogue to this day.

Angband is one of the more prominent Roguelike games. Started in 1990, the game has been developed ever since then, and remains a classic Roguelike gaming experience, though with modern improvements to smooth over some of Rogue’s original rough edges.

Installing Angband is pretty simple. Go to a Terminal window and use this command:

sudo apt-get install angband

Follow the default prompts and Angband will be installed. Once Angband is installed, you can start the game with this command:

angband

Follow the prompts to create your character and soon you’ll soon be playing. Watch out for the goblins!

DOSBOX

It is indeed a remarkable irony that it’s often no longer possible to play old DOS games on Windows 10, but with proper software, you can play the same old games on Linux Mint. All you need is DOSBox, an emulation environment that lets you run old DOS games. As an added bonus, DOSBox is quite easy to install. Simply go to a Terminal window and type this command:

sudo apt-get install dosbox

Follow the default prompts, and DOSBox will install itself and a few other necessary packages on your Linux Mint system. After DOSBox is installed, you can launch it by going the mintmenu and searching for "DOSBox" in the search field. Or you can launch it from the command line:

dosbox

Now, since DOSBox relies on the old DOS system of drive letters, and Linux Mint does not, you may be wondering how to mount your drives. Fortunately, this is quite simple. Let’s say you create a directory named dos in your home directory to serve as the C: drive during your DOS session. To mount as a C: drive, use this command while in DOSBox:

mount c ~/dos

To mount your optical drive as a D: drive, use this command:

mount d -t cdrom /media/cdrom

Using these commands, you should be able to play a good many old DOS games on your Linux Mint system.

STEAM

Valve made its popular Steam platform available for Linux Mint. Using the Steam client, you can play a number of popular games quite easily on your Linux Mint system (assuming your computer’s hardware meets the system requirements for the various games). Installing the Steam client on Linux Mint is an easy and streamlined process, and we’ll show you how to do it.

First, visit the Steam site and download the client:

http://store.steampowered.com

Click on the Install Steam button at the top of the page, and then the Install Steam Now button. This will download a .deb installer file to your Downloads folder. After the download has completed, navigate to your Downloads folder, and double-click on the installer to launch it.

After a moment the install will take you to the Linux Mint Software application and show you some information about Steam. Click on the Install button, and the Linux Mint Software application will ask for your password. Enter your password, and Linux Mint Software will install the client.

After the installation is complete, you can launch the Steam client by going to the mintmenu and searching for “Steam”. When the client launches for the first time, it will likely downloaded several hundred megabytes worth of updates.

Once the download is finished, you can log into the client and peruse your library of Steam games.

GOG.COM

One of the best developments for Linux gaming in the past ten years has been the rise of GOG.com. The site began as Good Old Games in 2008, devoted to acquiring the rights to legally sell "abandonware" games, old DOS games that had been abandoned by their publishers for whatever reason.

GOG.com 2008, originally Good Old Games, improved to GOG.com in 2010. GOG.com currently offers numerous older DOS games now repackaged to run smoothly on Linux Mint. In this example, we will show you how to install Darklands, a classic Microprose RPG from 1992\. The installation for Darklands is pretty typical, and you can use this example to install other older GOG.com games on Linux Mint.

First, log into your GOG.com account and download the Linux Mint installer for the game you wish to play. The installer will download as a shell script, which you will need to first mark as executable. To mark the shell script for Darklands as executable, launch the Terminal by hitting the CTRL+ATL+T keys simultaneously, and then enter this command

**chmod +x ~/Downloads/gog_darklands_2.0.0.7.sh**

Then execute the shell script with this command:

**~/Downloads/gog_darklands_2.0.0.7.sh**

This will launch the GOG.com installer for Darklands. Accept the EULA, and then select the destination folder for the installation. The default destinations are usually acceptable, unless you have a specific reason for installing the game elsewhere. The installer will then ask if you want to create a desktop shortcut and a menu item (this will allow you to find the game to launch it through the mintmenu). Make sure to select both, as it will make it easier to launch the game after the installer has finished.

Once the installation as finished, you can launch the game by going to the mintmenu, searching for "Darklands", and then double-clicking on the icon for Darklands. Linux Mint will then launch DOSBox and load Darklands preconfigured for you.

Note that the game will load full-screen – you can switch to the windowed mode by hitting the ALT and the ENTER keys simultaneously.

This procedure will let you install most of GOG.com's Linux Mint-compatible classic games.

GOG.com also has a number of newer games that run natively on Linux Mint. Be sure to check the system requirements, since they will display a list of any software packages you might need to run the game. You can usually install these packages from the Terminal with the **apt-get** command.

***

## Chapter 18 - Run Windows Software with Wine

I’ve helped many people try Linux Mint after switching from Windows, and they all inevitably have the same question.

“*Hey, Linux Mint is great! But how can I install my favorite Windows application on it?”*

On the surface, it seems like the obvious answer would be no. Windows software is written for the Windows platform, and Linux Mint software is written for the Linux platform, and never the two shall meet. If you want to use your favorite Windows application with Linux Mint, you need to either find a Linux version, or find another application that performs the task you want to do.

However, there’s a way around that.

That way is a software application called “Wine”, an acronym that means “Wine Is Not An Emulator.” It’s actually a compatibility layer that lets you, in theory, run Windows applications on a Linux system. Not all applications work, some work better than others, and some require considerable tweaking before they will work. However, if you’re willing to do the research, you can get your Windows application working on Linux Mint.

In the next section, we’ll look at installing and configuring Wine on an Linux Mint system. We’ll also talk a bit about using Linux Mint to connect to Windows Server Terminal Services / Remote Desktop Services systems.

INSTALLING AND CONFIGURING WINE

Configuring Wine can occasionally be a challenge, but Wine installs quite easily and runs just fine on Linux Mint. To install Wine, use this command at the Terminal prompt:

sudo apt-get install wine-stable

Enter your password to authenticate, and apt will download and install Wine. The combined packages come to a little over a hundred megabytes, so it might take a while to install depending upon your connection speed.

After the installation is finished, you can use the command line Wine program to install Windows software.

However, you’ll probably first need to mark the installer file as executable. Depending on the application, Wine might not be able to install it if its installer file isn’t executable. (We discussed file permissions in Chapter 2.) For instance, to mark an installer file in your Downloads folder named INSTALL.EXE as executable, use this command at the Terminal prompt:

chmod 755 ~/Downloads/INSTALL.EXE

After the file has been marked as executable, you can then install Windows software with Wine through the command line. For instance, to install the example above, you would use this command:

wine ~/Downloads/INSTALL.EXE

If the application did not install, you’ll probably have to change the Wine settings. The best course is to probably browse the Wine application database and see if you can find the correct settings there. The database contains settings and tips for installing thousands of Windows applications, and you can find it here:

http://appdb.winehq.org/

Generally, Wine is very good at backwards compatibility - the older an application is, the more likely it is that Wine will support it.

Finally, you can install a Windows application through a companion GUI application called Winetricks. Winetricks makes installing an application smooth and easy - but only if the specific application is supported. To install Winetricks, use this command at the Terminal:

sudo apt-get install winetricks

Once Winetricks is installed, you can launch it by going to the mintmenu, searching for "winetricks", and clicking on the icon for the application. Winetricks offers a GUI for installing Windows applications, and you can easily follow the prompts to install a supported Windows application.

INSTALL REMMINA

Microsoft Windows Servers have a technology called Terminal Services, renamed to Remote Desktop Services in Windows Server 2008 R2\. This allows client computers to remotely connect to the server, viewing the remote desktop and using the remote applications as if they were installed locally. Many organization use Terminal Services/ Remote Desktop Services to centralize their computing infrastructures. That way an organization can have a powerful central server system, and use cheaper client computers to connect to the Terminal Services / Remote Desktop Services server.

Every version of Windows since Windows XP comes with an included Remote Desktop client. However, Remote Desktop provides an opportunity for you to use Linux Mint in a Windows-heavy environment. Versions of Linux Mint prior to 11.04 Natty Narwhal used a program called TSclient as a Remote Desktop client. It worked, but not very well.

However, there’s a far superior option available now – Remmina. Linux Mint 11.04 Natty Narwhal (and all later versions of Linux Mint) includes Remmina as the default Remote Desktop client. Remmina has many more advanced features, and the biggest one is that it works much better on a netbook screen, and gives you greater options for selection the resolution. It also includes scroll bars for a Terminal Services window larger than the current screen size – an invaluable feature that TSClient just didn’t have. If you have an older version of Linux Mint, you can install Remmina with this command at the Terminal windows:

sudo apt-get install remmina

Enter your password to authenticate, and apt-get will download and install Remmina for you. After the installation is complete, you can launch Remmina by going to the Applications menu, to Internet, and clicking on the Remmina icon. In Linux Mint 11.04 Natty Narwhal, you can also launch Remmina by clicking on the mintmenu and searching for it in the search field.

***

## Chapter 19 - Managing and Creating eBooks on Linux Mint

This book only exists in ebook format, so if you’re reading it, you’re already familiar with ebooks as a concept. However, in the last few years (2007 to 2016, as of this writing), ebooks have taken the world by storm. Major online retailers report higher sales of ebooks than physical books, the sales of printed books and newspapers are collapsing, and bookstores are going out of business right and left. In my opinion, ebooks are as big a revolution as Gutenberg’s printing press or the invention of paper. And like the printing press, I think ebooks will result in a widespread increase in literacy, as an entire generation of men and women who have never purchased a physical book will nonetheless read on their computer screens or smartphones.

Fortunately, you can use Linux Mint to both manage and create ebooks, using a variety of free software tools that we will discuss in this chapter.

**WHAT IS AN EBOOK?**

An ebook, generally, is a book-length document stored in a digital file. Ebooks have been around almost since the beginning of the Internet – Project Gutenberg, which hosts an enormous number of free public domain ebooks, was founded in 1971\. Publishers have been experimenting with digital formats, mostly unsuccessfully, ever since the World Wide Web became popular in the late 1990s. However, the lack of a viable ereaders hampered early adoption of ebooks. Only a very few people enjoyed reading a full-length book on a CRT monitor or on the tiny screen of a PDA device.

This changed with the development of e-Ink and LED tablet devices towards the end of the first decade of the 21st century. A quality e-Ink reading device provides an experience almost as good as a printed page, and a decent LED display, while not as good as an e-Ink device for sustained reading, nonetheless is much easier to read than an old tube monitor. With the increasing ubiquity of Internet connections, and the decreasing cost of ereader devices, the ebook revolution is well underway.

Paper books will never go away – radio was superseded by first television and then the Internet, but there are no shortages of commercial radio stations – but ebooks offer a number of useful advantages over paper books. The first is portability – four gigabytes of flash memory can hold thousands of ebooks. The equivalent amount of paper books would fill several rooms. The second is a positive environmental impact – ebooks are far easier on the environment (and the forests, specifically) than paper books, and due to the antiquated returns system employed by most modern publishers and bookstores, thousands of paper books are wasted every year. The third advantage is cost – ebooks are often cheaper than their physical counterparts, and vast numbers of public domain books, including the classics of Western civilization, are available for free from Project Gutenberg and other sites.

**EBOOK FORMATS**

Ebooks come in a variety of formats, but there are two dominant ones – the MOBI format, and the EPUB format.

The MOBI format originated with a company called Mobipocket, which developed the MOBI format for ebooks and several different applications for reading MOBI files. Online retailer Amazon bought Mobipocket in 2005, and when the Kindle debuted in 2007, Amazon used the MOBI format for its Kindle books. Any ebook purchased off Amazon’s site will be in the MOBI format.

EPUB is the second dominant ebook format. Established in 2007, it evolved out of the old Open eBook standard. EPUB is an open standard, which means that anyone can use it without paying license fees. It is comparatively easy to work with, too, since it relies upon CSS and XHTML for the book layout. Barnes & Noble uses EPUB for their online store, along with Kobo, Google Play, and most of the other major ebook vendors.

(To generalize, Amazon uses MOBI, while pretty much everyone else uses EPUB.)

Because of this, there’s an annoying two-way split in the world of ebooks, much like the old fight over Betamax and VHS in the dawn of the VCR era. Many devices only read MOBI and not EPUB and vice-versa. Fortunately, a number of free tools exist to convert one format to another, which we shall discuss in the next section.

**CONVERT AND MANAGE EBOOKS WITH CALIBRE**

Because ebooks are often much cheaper than physical books, it is easy to quickly accumulate a large collection. Managing and organizing an ebook library can become something of a challenge. To make matters more complicated, the format war we discussed in the previous section means that some ebooks will work with one device, and others will not, and very few will work on both.

Fortunately, a free application called Calibre can solve a number of these problems. Originally developed in 2006, Calibre is an ebook management program. It automatically sorts your ebooks by title and author, which makes locating any single title much easier. It also can convert most ebook formats, allowing you to smoothly move from EPUB to MOBI and back again (so long as the files are not encrypted – Calibre cannot read ebook files protected by digital rights management technologies – DRM). Calibre also contains a built-in ebook reader that can handle most ebook formats.

Calibre is also very easy to install, and you can install it through the Linux Mint Software application. (We discussed how to use the Linux Mint Software application to install software in Chapter 4.) It is, of course, quicker and easier to install Calibre using this terminal command:

sudo apt-get install calibre

Enter your password to authenticate, follow the default prompts, and apt will install Calibre for you.

After the installation is complete, you can launch Calibre via searching for it through the mintmenu. The first time Calibre runs, you’ll see a wizard asking for some configuration options: where to store your Calibre library, what eBook reader you use (if any), and what settings that eBook reader uses. Enter the appropriate information, and you can start using Calibre.

Calibre's GUI is reasonably easy to use, and the program includes a complete manual (in ebook form, of course).

CREATE EBOOKS WITH SIGIL

Reading ebooks is simple enough, but suppose you want to create an ebook? Where do you start?

The free Sigil application is a WYSIWYG (“what you see is what you get”) editor that allows you to create EPUB files. Sigil is, as an application, fairly bare-bones, but with a bit of practice, you can create elaborate EPUB books with relative ease. (The EPUB version of this book was created with Sigil.) Sigil also lets you view the underlying XHTML code of an EPUB book, allowing you to make advanced changes to your book. Even better, it only takes a few terminal command to install Sigil on Linux Mint.

Here’s how to do it.

First, launch the Terminal by hitting the CTRL+ALT+T keys simultaneously, and then enter this command:

sudo apt-get install sigil

Enter your password to authenticate, and Linux Mint will download and install Sigil for you.

Once the installation is complete, you can launch Sigil by going to the mintmenu, searching for "Sigil", and clicking on its icon.

***

## Chapter 20 - Converting Audio and Video

Almost all modern computers are “multimedia” computers – that is, they can play sound and video. This was not always the case – early personal computers relied entirely upon text-based interfaces, and only gradually added support for images, sounds, and video playback. In Linux Mint, the text-based interface has not gone away (most of this book has discussed using the command line, after all), but a Linux Mint system is just as capable with multimedia as any Windows box or Macintosh laptop.

In this chapter we’ll discuss how to convert different multimedia formats, but first we’ll take a look at those multimedia formats themselves.

WHAT IS A FILE FORMAT?

When we talk about a multimedia file format, or a “codec”, we refer to a way of storing audio and video data in digital form. A sound or video is an analog form of data (basically, a long wave). Computers, however, store data in digital format – in long strings of ones and zeroes. A “codec”, therefore, is a piece of software that converts those ones and zeroes into an analog wave that you can play over your computer speakers.

As you might expect, there are many different standards for converting the ones and zeroes to analog waves and back again, and we’ll look at a few of those competing standards in the next section.

AUDIO FILE FORMATS

There are several competing formats for music and audio files. However, one of them is clearly dominant – the MP3 format. Developed in 1993 by the Moving Pictures Expert Group, MP3 is the most common format for digital music files. Almost all the major online retailers sell music files in MP3 format, and almost all operating systems either play MP3 files by default or can easily acquire the capacity to play them.

Despite its ubiquity, MP3 is encumbered with a number of legal problems. Due a complicated series of lawsuits, no one is entirely certain who owns some of the patents connected with MP3, so anyone wanting to use the MP3 codec with their software or hardware needs to pay a licensing fee.

Though MP3 is the major digital audio format, there are several other significant ones as well. Windows Media Audio, WMA, is the default media format for Microsoft Windows, and in the late 90s and early 2000s, Microsoft hoped it would replace MP3\. However, the Apple iPod came to dominate the digital music market during the 2000s, and Apple obviously had no interest in using one of Microsoft’s formats. These days, WMA tends to only play on Windows machines and devices, and little else.

AAC, Advanced Audio Coding, is another major audio format, as it is the default audio format for Apple’s iTunes software. AAC is designed to be the eventual replacement for the MP3 standard, and can compress more information into a smaller space than MP3.

A final major audio format is OGG/Vorbis. Unlike the other major formats mentioned here, OGG/Vorbis is free and open source, which means that companies can use it without paying licensing fees. Therefore Linux Mint supports it without any additional packages. However, OGG/Vorbis remains in the minority, and only a very small amount of digital media is available in the format.

VIDEO FILE FORMATS

Unlike audio file formats, there is not yet a single dominant video file format, but instead several major competing ones.

The oldest of the common video formats is Audio Video Interleave, or AVI. Introduced by Microsoft in the 1990s, AVI is comparatively primitive. Its biggest flaw is that it supports no compression whatsoever, which means that AVI files can become absolutely enormous. However, AVI works with numerous different applications and devices, so it remains in use.

WMV, Windows Media Video, is another major video format, the cousin to Microsoft’s Windows Media Audio format. WMV, unlike AVI, is compressed. Numerous digital camcorders make use of WMV by default, so it is quite common.

Another major format is the MP4 format, and is perhaps the most widely used format of the ones we will discuss here. A variant version of MP4 is the default format of Apple’s QuickTime software (known as MOV files), and due to the Macintosh’s popularity with video editing, MP4 files are quite common.

CONVERTING AUDIO WITH SOUND CONVERTER

If you have a WAV file that you want to convert to an MP3, it’s possible to do so quite easily and simply on a Linux Mint system. You just need one software package: the GNOME Sound Converter application. The Sound Converter program offers a GUI for converting sound files from one format to another.

To install the Sound Converter program itself, go to a Terminal window and type this command:

sudo apt-get install soundconverter

After you enter your password to authenticate, apt-get will download and install SoundConverter and its necessary dependencies. After the installation is complete, you can launch Sound Convert by going to the mintmenu, searching for “soundconverter”, and clicking on the Sound Converter icon.

Once the program has launched, go to the Edit menu, and to the Options item. From there you can set the kind of output you want the program to produce (OGG files, MP3 files, or AAC files), as well as the destination folder for the converted files. Once you’ve selected your preferences, hit the Close button, and then Add Files on the program’s main toolbar to choose the files you want to convert.

CONVERT AUDIO AND VIDEO WITH FFMPEG

From time to time you may need to extract the sound from a video file. Fortunately, using the ffmpeg program, it’s quite simple to take the sound from any video file and store it as a separate file. The ffmpeg utility can convert back and forth between multiple formats of both video and sound. Even better, in keeping with the overall theme of this book, ffmpeg is a command-line utility.

Use this command to install ffmpeg:

sudo apt-get install ffmpeg

After the installation is complete, you can use ffmpeg to extract the audio from a video file. Say, for example, you have a video file named test.avi. To extract the audio to a file named audio.mp3, use ffmpeg with these options and arguments:

ffmpeg -i test.avi audio.mp3

This will create an audio file named audio.mp3 containing the sound from the video file. However, by default ffmpeg creates audio files with a bitrate of 64 kbps, which results in very low-quality audio. To force ffmpeg to create the mp3 file at the 256 kbps bitrate, add the -ab option to the command:

ffmpeg -i test.avi -ab 256k audio.mp3

This will create a higher-quality mp3 file, and you can use this modified command to extract the audio from any compatible video file.

The ffmpeg utility can do many other conversions as well – be sure to read the entire manual page for ffmpeg with this command:

man ffmpeg

CONVERT VIDEO WITH HANDBRAKE

The popular Handbrake application is designed to convert DVD video into a format that portable media players can use, and can also do some video format conversion as well. Best of all, the installation only takes a few Terminal commands.

(Note that since Handbrake tends not to work on new versions of Linux Mint without an update, these directions may become out of date with the next version of Linux Mint.)

First, you’ll need to add Handbrake’s PPA (personal package archive) to your system. Go to a Terminal window and type this command:

sudo apt-get install handbrake

After the installation is complete, you can launch Handbrake by going to the mintmenu, searching for “Handbrake”, and clicking on the program’s icon.

VIEW MEDIA WITH VLC

(We already discussed installing VLC Media Player in Chapter 14, but it seems appropriate to repeat the information here.)

VLC Media Player is a handy program that can play numerous forms of video, and runs on just about any OS platform. It also runs on Linux Mint, and installing it is quite simple.

First, open up a Terminal window and type this command:

sudo apt-get install vlc

Enter your password to authenticate, and apt will download and install VLC and its various dependencies for you. (You can also install it through Synaptic Package Manager and Linux Mint Software Center.) Afterwards you can launch VLC by going to the mintmenu, searching for "VLC", and clicking on the VLC icon.

Of course, most of the media you watch will probably be found on the Internet, which means you’ll want the VLC plugins for Firefox. Fortunately, the VLC Firefox plug is also easy to install. Return to the Terminal and type this command:

sudo apt-get install vlc vlc-plugin-* mozilla-plugin-vlc

Once you enter your password, apt-get will install the Firefox VLC plugin. You can check that the plugin is installed by going to Firefox, to the Tools menu, and selecting Add-ons. Once in the Add-ons dialog box, you can view all your plugins by hitting the Plugins button. You should see the VLC plugins listed there.

***

## Chapter 21 - Managing Processes

We’ve already discussed process management a bit in an earlier chapter. However, monitoring processes – both keeping track of their resource usage and terminating them when necessary – is an important part of Linux Mint system administration. In this chapter we will discuss process management from the command line in more detail.

WHAT IS A PROCESS?

Technically speaking, a process is active instance of a computer program. So all the programs and applications you run on your Linux Mint machine are processes. For instance, if you were to run the Firefox web browser, and then execute the top command, you’ll see the “firefox” process displayed in the list of running process. When you exit the program, that process will exit and disappear. (Unless something goes wrong, which will discuss more with the section on the kill command.)

Processes are sometimes referred to as “daemons”, but the two terms aren’t identical. A daemon is in fact a process. However, the term “daemon” usually refers to a system process running in the background. The SSH daemon is one such background system process – it waits until it hears as SSH request over the network connection, regardless of what any standard users are currently doing on the system. Generally, system daemons have a “d” at the end of their names (the SSH daemon is named “sshd”) to distinguish them from processes that you or other users might have launched on the system.

First, we’ll discuss how to view currently running processes with the ps command.

THE PS COMMAND

Needless to say, administering your system requires you to keep a close eye on running processes. There are any number of commands and utilities for monitoring your system’s processes, but one of the simplest is the venerable ps command. To use the ps command, simply type it at the command prompt:

**ps**

However, without any switches, ps is not terribly useful. The default output without any switches looks like this:

![](tmp_38c39953b6c998474c8b24733c8ecdee_7h3Abx_html_544a2f77.jpg)

In its default state, ps only shows the currently running process – itself – and the shell you are currently using. Fortunately, you can make ps much more useful with the –e switch:

**ps –e**

The –e stands for Extended, and generates a listing of every process currently running on the system.

However, this still only displays a limited amount of information, especially when compared to the top command. You can tell the ps command to display more information with the –l switch:

**ps -el**

The –l switch stands for Long Listing, and generates quite a bit more information. Specifically, you can see the UID (user ID) of the user who launched the process, the PPID (parent PID) of the parent process of a child process, the process’s priority and nice, and numerous other useful pieces of information. For even more information, use ps with the –f switch:

**ps –elf**

In addition to the information offered by the –l switch, the addition of the –f switch also causes the ps command to display the date the process was launched and the location of its executable on the file system.

Even ps –elf is only a static snapshot of the processes currently running on the system. The running processes can change very quickly on a Linux system, and you might want to monitor them in real-time. That’s where the top command comes in.

THE TOP COMMAND

The top command has been around forever, and is included in practically every variant of Linux. Linux Mint is no exception. The top command displays a variety of useful statistics, including the “top” users of CPU time (hence the command’s name), the amount of memory running processes are using, the amount of virtual memory they are using, the process’s priority, the process’s owning user, and numerous other useful pieces of information. To launch top, simply type the command at the command prompt:

**top**

Once launched, top stays running, displaying statistics in real time. Processes are listed by their process ID number, along the name of the command that started the process.

There’s a lot of information listed in top, so let’s take a look at the available statistics:

PID: A process’s process ID number.

USER: The process’s owner. Processes owned by root are usually system processes, and should be left alone unless they cause problems.

PR: The process’s priority, which determines how much attention the CPU will give this process over other processes. The lower the number, the higher the priority.

NI: The nice value of the process, which affects its priority.

VIRT: How much virtual memory the process is using.

RES: How much physical RAM the process is using, measured in kilobytes.

SHR: How much shared memory the process is using.

S: The current status of the process (zombied, sleeping, running, uninterruptedly sleeping, or traced).

%CPU: The percentage of the processor time used by the process.

%MEM: The percentage of physical RAM used by the process.

TIME+: How much processor time the process has used.

COMMAND: The name of the command that started the process.

Of course, you may want to sort the top display by a certain category from least to greatest. This is especially useful when you want to figure out what process is hogging the most CPU time or memory. Hitting the ‘t’ key will sort the processes by CPU time. Hitting ‘l‘ will sort by load average, and ‘m‘ by memory info.

Like the GNOME System Monitor application, you can also use top to kill uncooperative processes. To do this, you’ll need to make note of the process ID you want to kill. Hit the “k” key while top is running, and the utility will ask you to input a process ID number. Input the number, hit Enter, and then hit Enter again when it asks if you want to kill the process (top assumes you mean “yes” when you hit enter). The top utility will then kill the process.

Once you’ve finished with top, hit the q key to exit and return to the command line.

Most often, you’ll use the top and ps commands to track down process that’s causing trouble. In the next section, we’ll discuss how to terminate troublesome processes with the (appropriately named) kill command.

THE KILL COMMAND

The kill command, as you might guess from the name, lets you kill running processes.

Technically, the kill command sends signals to running processes. However, this command is most commonly used to send the kill a running process. In most cases, you will use this command to terminate a process that has frozen up, refuses to quit gracefully, or is otherwise misbehaving. Using kill, you can terminate troublesome processes.

Note that to use kill, you need to know the PID (process identification number) of the process you wish to terminate. You can find out the PID using either the ps or the top commands (detailed elsewhere in this book).

To use kill, simply type the command with the PID of the targeted process. For instance, to terminate a process with the PID of 2589:

**kill 2589**

Like other commands, kill can be modified with a number of switches. Remember that kill operates by sending signals to the designated process. The kill command uses 64 separate signals, which you can list with the –l switch:

**kill –l**

Of those 64 signals, four of them are commonly used. You tell kill which signal to send by using the signal’s number as a switch – for instance, kill- 9 2589.

15 is the default kill signal. 15 tells the targeted process to cease immediately, but only after shutting down gracefully. Since 15 is the default kill signal, you don’t usually have explicity specify it, but if you did, the command to send the 15 signal to PID 2589 would look like this:

**kill -15 2589**

Signal number 1 less drastic. It merely tells the process to restart, while keeping the same PID. To use signal number 1:

**kill -1 2589**

Signal number 2 sends the CTRL+C character combination to a process, which is commonly used to break out of a running process (the ping command, for instance). To send signal number 2 to a process:

**kill -2 2589**

Finally, the most drastic signal is number 9\. Signal number 9 immediately kills a process, and does not give it the option to close gracefully or clean up after itself first. Generally, you should only use signal number 9 to terminate a process if nothing else has worked first:

**kill -9 2589**

Using ps, top, and kill, you can manage the running processes on your Linux Mint system from the command line, and quickly respond to any problems.

***

## Chapter 22 – Working With Documents From The Command Line

When working with “documents” (such as spreadsheets, presentations, PDF files, text documents, and the like), you will spend most of your time in Linux Mint’s graphical interface since most of the tools for working with documents are in the GUI. If you need to create an elaborate document or a complex spreadsheet, you will need to use a program in the GUI. (I suppose you could write a novel in the vi text editor, but it probably would not be a pleasant experience.)

That said, there are several command line utilities that allow you to automate certain document management tasks. For example, let’s say you have forty PDF files you need to merge into a single PDF document, or three hundred ODT documents you need to convert to HTML files. If you perform these tasks in the GUI, it will take a great deal of repetitive, tedious, and time-consuming pointing and clicking with the mouse. However, with a few well-chosen commands, you can easily handle several tedious document-management tasks.

MANAGE PDF FILES WITH PDFTK

PDF stands for Portable Document Format, and has become the de facto standard for official government documents and corporate documents – think of how many times you have had to visit a government website or your employer’s website to download and fill out an official form in PDF. The upside to this is that a document creator can arrange to have a PDF look exactly the way he wants it, since PDFs are readable on many different operating systems and devices. The downside is that if you need to change a PDF file after it has been created, changing it is both annoying and difficult.

The is where the pdftk utility comes into play. The pdftk utility (it’s short for “PDF Toolkit”) allows you to combine and separate PDF files. It’s not included in the default installation of Linux Mint, but you can rectify that in short order from the command line. Log into an account with administrative rights, go to a Terminal window, and type this command:

sudo apt-get install pdftk

Enter your password to authenticate, and apt will download and install pdftk for you. After the installation is complete, you can use pdftk from the command line.

Now that you have pdftk installed, we’ll show you how to use it combine PDF files. Let’s say, for example, that you have three PDF files: Page1.pdf, Page2.pdf, and Page3.pdf. You need to combine them into a single PDF document called FinalDraft.pdf. You could do this via LibreOffice or another document editing program. Or you could do it with pdftk:

pdftk Page1.pdf Page2.pdf Page3.pdf output FinalDraft.pdf

This command will take the three PDF files and combine them into a single PDF named FinalDraft.pdf. Note that pdftk will combine the files in the order they are listed. So if you wanted Page3.pdf to actually be the first page in FinalDraft.pdf instead of Page1.pdf, you would use this command:

pdftk Page3.pdf Page2.pdf Page1.pdf output FinalDraft.pdf

This will create the FinalDraft.pdf document with the Page3.pdf as its first page.

You can also use pdftk to extract single pages from larger PDF documents. In this example, let’s say you have a 90-page PDF document named Report.pdf. You want to extract only page 9 from this document so you can email it to a coworker. To extract page 9 from Report.pdf and save it as its own PDF document named Page9.pdf, use pdftk with these options:

pdftk A=Report.pdf cat A9 output Page9.pdf

This will take the ninth page from Report.pdf and save it as its own PDF document named Page9.pdf.

Likewise, you can also use pdftk to extract a range of pages from a PDF document and save them in their own file. To return to our previous example, if you wanted to extract pages 19 through 37 of Report.pdf in their own file named Extract.pdf, you would use pdftk with these options:

pdftk A=Report.pdf cat A19-37 output Extract.pdf

With pdftk, you can disassemble and reassemble PDF documents with ease.

CONVERTING FILE TYPES WITH LIBREOFFICE

LibreOffice, the free office suite included with Linux Mint, has a fairly useful feature that’s not very well known. Called “headless mode”, this allows you to run LibreOffice from the command line without launching any graphical interface components. Since LibreOffice is a full-featured office suite, this might seem like a waste of time. However, you can use LibreOffice’s headless mode to perform batch conversions of files. Using it to convert, say, one *.doc file to a PDF document might seem cumbersome. However, if you have 2,000 *.doc files you need to convert to PDFs (as part of, to cite a common example, government regulatory compliance), this can save a tremendous amount of time.

In our first example, let’s say you have 1,000 *.doc files you need to convert to PDFs. The document files are located in a directory called “source” in your home directory, and you want to have the PDFs in a directory called “output” in your home directory. The command to convert the doc files to PDF files will look like this:

**libreoffice –headless –convert-to pdf:writer_pdf_Export -outdir ~/output ~/source/*.doc**

This will take every single *.doc file in the ~/source directory and convert it to a corresponding PDF file in the ~/source directory. Note that the original *.doc files are not altered in any way.

You can also use this command to perform mass conversions of other file formats. For instance, let’s say you wanted to turn those 1,000 *.doc files into HTML files instead. The command would look like this:

libreoffice –headless –convert-to html -outdir ~/output ~/source/*.doc

This will convert the *.doc files in ~/output to HTML files in ~/source. Again, the original document files will not be altered.

By changing the parameter after the –convert-to option, you can convert to and from any of the file types supported by LibreOffice. If you wanted to change your *.doc files in ~/source to *.odt files (OpeDocument Format files), the command would look like this:

libreoffice –headless –convert-to odt -outdir ~/output ~/source/*.doc

Using LibreOffice’s command-line utility allows you to quickly and easily perform batch conversions of documents.

***

## Other books by the author

The Demonsouled Saga

MAZAEL CRAVENLOCK is a wandering knight, fearless in battle and masterful with a sword.

Yet he has a dark secret. He is Demonsouled, the son of the ancient and cruel Old Demon, and his tainted blood grants him superhuman strength and speed. Yet with the power comes terrible, inhuman rage, and Mazael must struggle to keep the fury from devouring him.

But he dare not turn aside from the strength of his blood, for he will need it to face terrible foes.

The priests of the San-keth plot and scheme in the shadows, pulling lords and kingdoms upon their strings. The serpent priests desire to overthrow the realms of men and enslave humanity. Unless Mazael stops them, they shall force all nations to bow before the serpent god.

The Malrag hordes are coming, vast armies of terrible, inhuman beasts, filled with a lust for cruelty and torment. The Malrags care nothing for conquest or treasure, only slaughter. And the human realms are ripe for the harvest. Only a warrior of Mazael’s power can hope to defeat them.

The Dominiar Order and the Justiciar Order were once noble and respected, dedicated to fighting the powers of dark magic. Now they are corrupt and cynical, and scheme only for power and glory. They will kill anyone who stands in their way.

To defeat these foes, Mazael will need all the strength of his Demonsouled blood.

Yet he faces a far more terrible foe.

For centuries the Old Demon has manipulated kings and lords. Now he shall seize the power of the Demonsouled for himself, and become the a god of torment and tyranny.

Unless Mazael can stop him.

Read [Demonsouled](http://www.jonathanmoeller.com/writer/?page_id=880) (http://www.jonathanmoeller.com/writer/?page_id=880) for free. Mazael's adventures continue in [Soul of Tyrants](http://www.jonathanmoeller.com/writer/?page_id=911) (http://www.jonathanmoeller.com/writer/?page_id=911), [Soul of Serpents](http://www.jonathanmoeller.com/writer/?page_id=1287) (http://www.jonathanmoeller.com/writer/?page_id=1287), [Soul of Dragons](http://www.jonathanmoeller.com/writer/?page_id=1727) (http://www.jonathanmoeller.com/writer/?page_id=1727), [Soul of Sorcery](http://www.jonathanmoeller.com/writer/?page_id=1845) (http://www.jonathanmoeller.com/writer/?page_id=1845), [Soul of Skulls](http://www.jonathanmoeller.com/writer/?page_id=2808) (http://www.jonathanmoeller.com/writer/?page_id=2808), and [Soul of Swords](http://www.jonathanmoeller.com/writer/?page_id=3599) (http://www.jonathanmoeller.com/writer/?page_id=3599), along with the short stories [The Wandering Knight](http://www.jonathanmoeller.com/writer/?page_id=3073) (http://www.jonathanmoeller.com/writer/?page_id=3073), [The Tournament Knight](http://www.jonathanmoeller.com/writer/?page_id=3677) (http://www.jonathanmoeller.com/writer/?page_id=3677), and [The Dragon's Shadow](http://www.jonathanmoeller.com/writer/?page_id=2635) (http://www.jonathanmoeller.com/writer/?page_id=2635). Get the first three books bundled together in [Demonsouled Omnibus One](http://www.jonathanmoeller.com/writer/?page_id=4442) (http://www.jonathanmoeller.com/writer/?page_id=4442).

The Ghosts Series

Once CAINA AMALAS was the shy daughter of a minor nobleman, content to spend her days in her father’s library.

Then sorcery and murder and her mother’s treachery tore her life apart.

Now she is a nightfighter of the Ghosts, an elite agent of the spies and assassins of the Emperor of Nighmar. She is a master of disguise and infiltration, of stealth and the shadows.

And she will need all those skills to defend the Empire and stay alive.

Corrupt lords scheme and plot in the shadows, desiring to pull down the Emperor and rule the Empire for their own profit and glory. Slave traders lurk on the fringes of the Empire, ready to seize unwary commoners and sell them into servitude in distant lands. Yet both slave traders and cruel lords must beware the Ghosts.

The Magisterium, the Imperial brotherhood of sorcerers, believe themselves the rightful masters of the Empire. With their arcane sciences, they plan to overthrow the Empire and enslave the commoners, ruling all of mankind for their own benefit. Only the Ghosts stand in the path of their sinister plans.

And the Moroaica, the ancient sorceress of legend and terror, waits in the shadows, preparing to launch a war upon the gods themselves. She will make the gods pay for the suffering of mankind...even if she must destroy the world to do it.

Caina Amalas of the Ghosts opposes these mighty enemies, but the cost might be more than she can bear.

Read [Child of the Ghosts](http://www.jonathanmoeller.com/writer/?page_id=1057) (http://www.jonathanmoeller.com/writer/?page_id=1057) for free. Caina's adventures continue in [Ghost in the Flames](http://www.jonathanmoeller.com/writer/?page_id=1265) (http://www.jonathanmoeller.com/writer/?page_id=1265), [Ghost in the Blood](http://www.jonathanmoeller.com/writer/?page_id=1383) (http://www.jonathanmoeller.com/writer/?page_id=1383), [Ghost in the Storm](http://www.jonathanmoeller.com/writer/?page_id=1931) (http://www.jonathanmoeller.com/writer/?page_id=1931), [Ghost in the Stone](http://www.jonathanmoeller.com/writer/?page_id=2520) (http://www.jonathanmoeller.com/writer/?page_id=2520), [Ghost in the Forge](http://www.jonathanmoeller.com/writer/?page_id=3181) (http://www.jonathanmoeller.com/writer/?page_id=3181), [Ghost in the Ashes](http://www.jonathanmoeller.com/writer/?page_id=3932) (http://www.jonathanmoeller.com/writer/?page_id=3932), [Ghost in the Mask](http://www.jonathanmoeller.com/writer/?page_id=4231) (http://www.jonathanmoeller.com/writer/?page_id=4231), and [Ghost in the Surge](http://www.jonathanmoeller.com/writer/?page_id=4637) (http://www.jonathanmoeller.com/writer/?page_id=4637), along with the short stories [Ghost Aria](http://www.jonathanmoeller.com/writer/?page_id=3243) (http://www.jonathanmoeller.com/writer/?page_id=3243), [Ghost Claws](http://www.jonathanmoeller.com/writer/?page_id=3930) (http://www.jonathanmoeller.com/writer/?page_id=3930), [Ghost Omens](http://www.jonathanmoeller.com/writer/?page_id=4235) (http://www.jonathanmoeller.com/writer/?page_id=4235), [The Fall of Kyrace](http://www.jonathanmoeller.com/writer/?page_id=4258) (http://www.jonathanmoeller.com/writer/?page_id=4258), [Ghost Thorns](http://www.jonathanmoeller.com/writer/?page_id=4639) (http://www.jonathanmoeller.com/writer/?page_id=4639), [Ghost Undying](http://www.jonathanmoeller.com/writer/?page_id=4662) (http://www.jonathanmoeller.com/writer/?page_id=4662), [Ghost Light](http://www.jonathanmoeller.com/writer/?page_id=5653) (http://www.jonathanmoeller.com/writer/?page_id=5653), and [Ghost Dagger](http://www.jonathanmoeller.com/writer/?page_id=2371) (http://www.jonathanmoeller.com/writer/?page_id=2371), and the prequel novels [Blade of the Ghosts](http://www.jonathanmoeller.com/writer/?page_id=6220) (http://www.jonathanmoeller.com/writer/?page_id=6220) and [Champion of the Ghosts](http://www.jonathanmoeller.com/writer/?page_id=6304) (http://www.jonathanmoeller.com/writer/?page_id=6304). Get the first three books bundled together in [The Ghosts Omnibus One](http://www.jonathanmoeller.com/writer/?page_id=4484) (http://www.jonathanmoeller.com/writer/?page_id=4484).

The Ghost Exile Series

Caina Amalas was a nightfighter of the Ghosts, the spies and assassins of the Emperor of Nighmar, and through her boldness and cunning saved the Empire and the world from sorcerous annihilation.

But the victory cost her everything.

Now she is exiled and alone in the city of Istarinmul, far from her home and friends. Yet a centuries-old darkness now stirs in Istarinmul, eager to devour the city and the world itself.

And Caina is the only one that stands in its way...

Read [Ghost in the Cowl](http://www.jonathanmoeller.com/writer/?page_id=4903) (http://www.jonathanmoeller.com/writer/?page_id=4903), [Ghost in the Maze](http://www.jonathanmoeller.com/writer/?page_id=5090) (http://www.jonathanmoeller.com/writer/?page_id=5090), [Ghost in the Hunt](http://www.jonathanmoeller.com/writer/?page_id=5244) (http://www.jonathanmoeller.com/writer/?page_id=5244), [Ghost in the Razor](http://www.jonathanmoeller.com/writer/?page_id=5553) (http://www.jonathanmoeller.com/writer/?page_id=5553), [Ghost in the Inferno](http://www.jonathanmoeller.com/writer/?page_id=5759) (http://www.jonathanmoeller.com/writer/?page_id=5759), [Ghost in the Seal](http://www.jonathanmoeller.com/writer/?page_id=5924) (http://www.jonathanmoeller.com/writer/?page_id=5924), [Ghost in the Throne](http://www.jonathanmoeller.com/writer/?page_id=6145) (http://www.jonathanmoeller.com/writer/?page_id=6145), [Ghost in the Pact](http://www.jonathanmoeller.com/writer/?page_id=6629) (http://www.jonathanmoeller.com/writer/?page_id=6629), and [Ghost in the Winds](http://www.jonathanmoeller.com/writer/?page_id=6694) (http://www.jonathanmoeller.com/writer/?page_id=6694) along with the short stories [Ghost Sword](http://www.jonathanmoeller.com/writer/?page_id=4911) (http://www.jonathanmoeller.com/writer/?page_id=4911), [Ghost Price](http://www.jonathanmoeller.com/writer/?page_id=5105) (http://www.jonathanmoeller.com/writer/?page_id=5105), [Ghost Relics](http://www.jonathanmoeller.com/writer/?page_id=5265) (http://www.jonathanmoeller.com/writer/?page_id=5265), [Ghost Keeper](http://www.jonathanmoeller.com/writer/?page_id=5481) (http://www.jonathanmoeller.com/writer/?page_id=5481), [Ghost Nails](http://www.jonathanmoeller.com/writer/?page_id=5504) (http://www.jonathanmoeller.com/writer/?page_id=5504), [Ghost Lock](http://www.jonathanmoeller.com/writer/?page_id=5776) (http://www.jonathanmoeller.com/writer/?page_id=5776), [Ghost Arts](http://www.jonathanmoeller.com/writer/?page_id=5937) (http://www.jonathanmoeller.com/writer/?page_id=5937), [Ghost Vigil](http://www.jonathanmoeller.com/writer/?page_id=6153) (http://www.jonathanmoeller.com/writer/?page_id=6153), [Ghost Mimic](http://www.jonathanmoeller.com/writer/?page_id=6648) (http://www.jonathanmoeller.com/writer/?page_id=6648), and [Ghost Vessel](http://www.jonathanmoeller.com/writer/?page_id=7028) (http://www.jonathanmoeller.com/writer/?page_id=7028), and read the combined short stories in [Exile of the Ghosts](http://www.jonathanmoeller.com/writer/?page_id=7936) (http://www.jonathanmoeller.com/writer/?page_id=7936).

The Ghost Night Series

Caina Amalas was once a deadly Ghost nightfighter, a spy and agent of the Emperor of Nighmar. Now she only wishes to live quietly with her husband.

But civil war grips the Empire, and Caina's skills are needed against the cruel sorcerers of the malevolent Umbarian Order.

And Caina has a dangerous connection to the Umbarians.

For Caina's mother had many deadly secrets, secrets that might yet kill Caina herself...

Read [Ghost in the Ring](http://www.jonathanmoeller.com/writer/?page_id=7928) (http://www.jonathanmoeller.com/writer/?page_id=7928).

The Third Soul

RACHAELIS MORULAN is an Initiate of the Conclave, the powerful order of mighty mages. But to become a full Adept of the Conclave, she must first survive the Testing. Those who survive the Testing never speak of the trials they endured.

Those who fail the Testing are never seen again.

And now the Magisters of the Conclave have come to take Rachaelis to undertake the Testing. And there she shall face perils to both her body and her sanity.

And creatures that yearn to devour her soul.

If Rachaelis survives the Testing, she will face even more dangerous foes. The demons of the astral world watch the world of mortal men, desiring to rule it for themselves.

And some Adepts of the Conclave are eager to help them.

Read [The Testing](http://www.jonathanmoeller.com/writer/?page_id=1538) (http://www.jonathanmoeller.com/writer/?page_id=1538) for free. Rachelis's trials continue in [The Assassins](http://www.jonathanmoeller.com/writer/?page_id=1540) (http://www.jonathanmoeller.com/writer/?page_id=1540), [The Blood Shaman](http://www.jonathanmoeller.com/writer/?page_id=1542) (http://www.jonathanmoeller.com/writer/?page_id=1542), [The High Demon](http://www.jonathanmoeller.com/writer/?page_id=1544) (http://www.jonathanmoeller.com/writer/?page_id=1544), [The Burning Child](http://www.jonathanmoeller.com/writer/?page_id=2756) (http://www.jonathanmoeller.com/writer/?page_id=2756), [The Outlaw Adept](http://www.jonathanmoeller.com/writer/?page_id=3341) (http://www.jonathanmoeller.com/writer/?page_id=3341), [The Black Paladin](http://www.jonathanmoeller.com/writer/?page_id=3343) (http://www.jonathanmoeller.com/writer/?page_id=3343), and [The Tomb of Baligant](http://www.jonathanmoeller.com/writer/?page_id=3345) (http://www.jonathanmoeller.com/writer/?page_id=3345). Read the entire series in [The Third Soul Omnibus One](http://www.jonathanmoeller.com/writer/?page_id=4021) (http://www.jonathanmoeller.com/writer/?page_id=4021) and [The Third Soul Omnibus Two](http://www.jonathanmoeller.com/writer/?page_id=4061) (http://www.jonathanmoeller.com/writer/?page_id=4061).

The Frostborn Series

A thousand years ago, the last grandson of Arthur Pendragon led the survivors of Britain through a magical gate to a new world, a world of magic and high elves, of orcs and kobolds and stranger, darker creatures. Now the descendants of the exiles rule a mighty kingdom, peaceful and prosperous under the rule of the High King.

But a shadow threatens to devour the kingdom.

RIDMARK ARBAN was once a Swordbearer, a knight of renown. Now he is a branded outcast, stripped of his sword, and despised as a traitor.

But he alone sees the danger to come. The Frostborn shall return, and unless they are stopped, they will cover all the world in ice and a neverending winter.

CALLIANDE awakens in the darkness, her memories gone, and creatures of terrible power hunting her.

For she alone holds the secret that can save the world…or destroy it utterly.

The secret of the Frostborn.

Read [Frostborn: The First Quest](http://www.jonathanmoeller.com/writer/?page_id=4439) (http://www.jonathanmoeller.com/writer/?page_id=4439), followed by [Frostborn: The Gray Knight](http://www.jonathanmoeller.com/writer/?page_id=4069) (http://www.jonathanmoeller.com/writer/?page_id=4069), [Frostborn: The Eightfold Knife](http://www.jonathanmoeller.com/writer/?page_id=4437) (http://www.jonathanmoeller.com/writer/?page_id=4437), [Frostborn: The Undying Wizard](http://www.jonathanmoeller.com/writer/?page_id=4776) (http://www.jonathanmoeller.com/writer/?page_id=4776), [Frostborn: The Master Thief](http://www.jonathanmoeller.com/writer/?page_id=5007) (http://www.jonathanmoeller.com/writer/?page_id=5007), [Frostborn: The Iron Tower](http://www.jonathanmoeller.com/writer/?page_id=5183) (http://www.jonathanmoeller.com/writer/?page_id=5183), [Frostborn: The Dark Warden](http://www.jonathanmoeller.com/writer/?page_id=5330) (http://www.jonathanmoeller.com/writer/?page_id=5330), [Frostborn: The Gorgon Spirit](http://www.jonathanmoeller.com/writer/?page_id=5330) (http://www.jonathanmoeller.com/writer/?page_id=5330), [Frostborn: The Broken Mage](http://www.jonathanmoeller.com/writer/?page_id=5860) (http://www.jonathanmoeller.com/writer/?page_id=5860), [Frostborn: The World Gate](http://www.jonathanmoeller.com/writer/?page_id=6028) (http://www.jonathanmoeller.com/writer/?page_id=6028), [Frostborn: The High Lords](http://www.jonathanmoeller.com/writer/?page_id=6403) (http://www.jonathanmoeller.com/writer/?page_id=6403), [Frostborn: The False King](http://www.jonathanmoeller.com/writer/?page_id=6865) (http://www.jonathanmoeller.com/writer/?page_id=6865), [Frostborn: The Dwarven Prince](http://www.jonathanmoeller.com/writer/?page_id=7270) (http://www.jonathanmoeller.com/writer/?page_id=7270), [Frostborn: Excalibur](http://www.jonathanmoeller.com/writer/?page_id=7414) (http://www.jonathanmoeller.com/writer/?page_id=7414), [Frostborn: The Dragon Knight](http://www.jonathanmoeller.com/writer/?page_id=7549) (http://www.jonathanmoeller.com/writer/?page_id=7549), and [Frostborn: The Shadow Prison](http://www.jonathanmoeller.com/writer/?page_id=7803) (http://www.jonathanmoeller.com/writer/?page_id=7803), and the prequel novels [Frostborn: The Knight Quests](http://www.jonathanmoeller.com/writer/?page_id=6384) (http://www.jonathanmoeller.com/writer/?page_id=6384) and [Frostborn: The Bone Quest](http://www.jonathanmoeller.com/writer/?page_id=8069) (http://www.jonathanmoeller.com/writer/?page_id=8069) along with the short stories [The Orc's Tale](http://www.jonathanmoeller.com/writer/?page_id=5661) (http://www.jonathanmoeller.com/writer/?page_id=5661), [The Mage's Tale](http://www.jonathanmoeller.com/writer/?page_id=4784) (http://www.jonathanmoeller.com/writer/?page_id=4784), [The Thief's Tale](http://www.jonathanmoeller.com/writer/?page_id=5012) (http://www.jonathanmoeller.com/writer/?page_id=5012), [The Assassin's Tale](http://www.jonathanmoeller.com/writer/?page_id=5186) (http://www.jonathanmoeller.com/writer/?page_id=5186), [The Paladins's Tale](http://www.jonathanmoeller.com/writer/?page_id=5328) (http://www.jonathanmoeller.com/writer/?page_id=5328), [The Knight's Tale](http://www.jonathanmoeller.com/writer/?page_id=5865) (http://www.jonathanmoeller.com/writer/?page_id=5865), [The Soldier's Tale](http://www.jonathanmoeller.com/writer/?page_id=6045) (http://www.jonathanmoeller.com/writer/?page_id=6045), and [The Soldier's Tale](http://www.jonathanmoeller.com/writer/?page_id=6409) (http://www.jonathanmoeller.com/writer/?page_id=6409). Read the first three books combined in [Frostborn Omnibus One](http://www.jonathanmoeller.com/writer/?page_id=5671) (http://www.jonathanmoeller.com/writer/?page_id=5671).

Sevenfold Sword

Ridmark Arban is the Shield Knight, the defender of the realm of Andomhaim.

The realm is at peace after a long and terrible war, but dark powers threaten other lands.

And when a mad elven wizard comes to the High King's court, Ridmark finds himself fighting not only for his own life, but for the lives of his family.

For the quest of the Seven Swords has begun...

Read [Sevenfold Sword: Champion](http://www.jonathanmoeller.com/writer/?page_id=7831) (http://www.jonathanmoeller.com/writer/?page_id=7831) and [Sevenfold Sword: Swordbearer](http://www.jonathanmoeller.com/writer/?page_id=8067) (http://www.jonathanmoeller.com/writer/?page_id=8067), and the prequel novella [Shield Knight: Ghost Orcs](http://www.jonathanmoeller.com/writer/?page_id=8269) (http://www.jonathanmoeller.com/writer/?page_id=8269).

Mask of the Demonsouled Trilogy

MAZAEL CRAVENLOCK has prevailed over terrible foes and now rules the Grim Marches with firm justice. Yet ancient evils are stirring in the shadows, freed at last by Mazael's own hand. Unless Mazael fights with all his strength, the world will fall.

SIGALDRA is the last holdmistress of the Jutai nation, the final defender of her people. Now the darkness comes to devour the final remnant of Sigaldra's home and family. Even Sigaldra's courage may not be enough to turn aside the darkness.

Read [Mask of Swords](http://www.jonathanmoeller.com/writer/?page_id=5429) (http://www.jonathanmoeller.com/writer/?page_id=5429), [Mask of Dragons](http://www.jonathanmoeller.com/writer/?page_id=6511) (http://www.jonathanmoeller.com/writer/?page_id=6511), and [Mask of Spells](http://www.jonathanmoeller.com/writer/?page_id=7196) (http://www.jonathanmoeller.com/writer/?page_id=7196) along with the short stories [The Ransom Knight](http://www.jonathanmoeller.com/writer/?page_id=5446) (http://www.jonathanmoeller.com/writer/?page_id=5446), [The Bronze Knight](http://www.jonathanmoeller.com/writer/?page_id=6531) (http://www.jonathanmoeller.com/writer/?page_id=6531), [The Serpent Knight](http://www.jonathanmoeller.com/writer/?page_id=5856) (http://www.jonathanmoeller.com/writer/?page_id=5856), and [The Rune Knight](http://www.jonathanmoeller.com/writer/?page_id=7183) (http://www.jonathanmoeller.com/writer/?page_id=7183).

The Tower of Endless Worlds

THOMAS WYCLIFFE just wants to finish his dissertation in peace and quiet. So when a man in a black robe appears in his closet, claiming to be the last of the Warlocks, Wycliffe figures it is a bad joke.

But he soon realizes the last of the Warlocks can give him power beyond imagining.

And all it will cost is his soul.

SIMON WESTER needs a job. Badly. So when a rich and powerful Senator offers him employment, he jumps at the chance. Sure, Simon expects to find some corruption, some shady deals.

He doesn't expect to find black magic.

LIAM MASTERE is a Knight of the Sacred Blade, defender of the mortal races. But can swords stand against guns? As bullets and bombs destroy his kingdom, Liam must risk everything to save his homeland's one chance of salvation.

By daring the horrors of the Tower of Endless Worlds…

Read [The Tower of Endless Worlds](http://www.jonathanmoeller.com/writer/?page_id=2073) (http://www.jonathanmoeller.com/writer/?page_id=2073) for free. The saga of the Tower continues in [A Knight of the Sacred Blade](http://www.jonathanmoeller.com/writer/?page_id=2076) (http://www.jonathanmoeller.com/writer/?page_id=2076), [A Wizard of the White Council](http://www.jonathanmoeller.com/writer/?page_id=2078) (http://www.jonathanmoeller.com/writer/?page_id=2078), and [The Destroyer of Worlds](http://www.jonathanmoeller.com/writer/?page_id=2080) (http://www.jonathanmoeller.com/writer/?page_id=2080).

Cloak Games

In 2013, a gate to another world opened, and Elves used their magic to conquer Earth, crushing all resistance before them.

Three hundred years after the Conquest, the exiled Elven High Queen rules an orderly but stagnant Earth, with humanity forced to fight in the High Queen’s war against the traitors on the Elven homeworld.

Nadia Moran doesn’t care about that. She doesn’t care about the High Queen, or the Rebels seeking to overthrow her. All she cares about is getting her baby brother the treatments he needs to recover from his potentially fatal disease…and those treatments have a steep price.

Fortunately, Nadia has magic of her own, and she’s a very, very good thief.

Unfortunately, the powerful Elven lord Morvilind has a hold on Nadia. If she doesn’t follow his commands, her brother is going to die.

Of course, given how dangerous Morvilind’s missions are, Nadia might not live long enough to see her brother’s death…

Read [Cloak Games: Thief Trap](http://www.jonathanmoeller.com/writer/?page_id=5969) (http://www.jonathanmoeller.com/writer/?page_id=5969), [Cloak Games: Frost Fever](http://www.jonathanmoeller.com/writer/?page_id=6072) (http://www.jonathanmoeller.com/writer/?page_id=6072), [Cloak Games: Rebel Fist](http://www.jonathanmoeller.com/writer/?page_id=6225) (http://www.jonathanmoeller.com/writer/?page_id=6225), [Cloak Games: Shadow Jump](http://www.jonathanmoeller.com/writer/?page_id=6713) (http://www.jonathanmoeller.com/writer/?page_id=6713), [Cloak Games: Shatter Stone](http://www.jonathanmoeller.com/writer/?page_id=7325) (http://www.jonathanmoeller.com/writer/?page_id=7325), [Cloak Games: Truth Chain](http://www.jonathanmoeller.com/writer/?page_id=7426) (http://www.jonathanmoeller.com/writer/?page_id=7426), [Cloak Games: Tomb Howl](http://www.jonathanmoeller.com/writer/?page_id=7598) (http://www.jonathanmoeller.com/writer/?page_id=7598), and [Cloak Games: Hammer Break](http://www.jonathanmoeller.com/writer/?page_id=8121) (http://www.jonathanmoeller.com/writer/?page_id=8121), along with the short stories [Wraith Wolf](http://www.jonathanmoeller.com/writer/?page_id=6735) (http://www.jonathanmoeller.com/writer/?page_id=6735), [Dragon Pearl](http://www.jonathanmoeller.com/writer/?page_id=7473) (http://www.jonathanmoeller.com/writer/?page_id=7473), and [Iron Image](http://www.jonathanmoeller.com/writer/?page_id=8142) (http://www.jonathanmoeller.com/writer/?page_id=8142).

***

## About the Author

Standing over six feet tall, *USA Today* bestselling author Jonathan Moeller has the piercing blue eyes of a Conan of Cimmeria, the bronze-colored hair of a Visigothic warrior-king, and the stern visage of a captain of men, none of which are useful in his career as a computer repairman, alas.

He has written the DEMONSOULED series of sword-and-sorcery novels, and continues to write THE GHOSTS sequence about assassin and spy Caina Amalas, the COMPUTER BEGINNER'S GUIDE series of computer books, and numerous other works. His books have sold over three quarters of a million copies worldwide.

Visit his website at:

[http://www.jonathanmoeller.com](http://www.jonathanmoeller.com/)

Visit his technology blog at:

[http://www.computerbeginnersguides.com](http://www.computerbeginnersguides.com/)

Contact him at:

jmcontact@jonathanmoeller.com

You can [sign up for his email newsletter here](http://www.jonathanmoeller.com/writer/?page_id=1854) (http://www.jonathanmoeller.com/writer/?page_id=1854), or watch for news on his [Facebook page](http://www.facebook.com/pages/Jonathan-Moeller/328773987230189) (http://www.facebook.com/pages/Jonathan-Moeller/328773987230189) or [Twitter feed](https://twitter.com/moellerjonathan) (https://twitter.com/moellerjonathan).

***