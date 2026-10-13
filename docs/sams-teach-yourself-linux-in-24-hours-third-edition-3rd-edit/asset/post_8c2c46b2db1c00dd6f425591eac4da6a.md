
After you've selected packages, it's time to take a break and let the computer do some work. Depending on the packages you selected and the speed of your computer, it might take anywhere from 15 to 45 minutes to install all the software. As the software is installed, you can watch the progress. As each package is installed, you'll see the name of the package and a brief description.

## Configuring the System

Now is the time to tell the installation process how you want to use the computer. Some of these steps can be skipped if you don't want to deal with them right now. You can always go back later to set up your Internet connection or attach a printer to the computer.

You will be asked whether you want to configure networking. If the computer is attached to a local area network, you will need some information from the system administrator (such as a name for the computer and the IP address). If the computer will be used to connect to the Internet, you can create a dialup connection now, or you can wait until Hour 21, "Connecting to the Internet," to learn how to set up a modem and connect to your ISP.

To set the clock correctly, the operating system needs to know the time zone in which you live. Scroll through the list and find the city closest to you.

If a printer is attached to the computer, you can configure printing services at this time, or you can wait until Hour 11, "Printing Files," to set up the printer.

You are next asked to assign a password to the root account. The root account, or superuser, is the system administrator for the operating system. This account has no restrictions; this enables the superuser to do anything she wants to the system. This account should be used only for system maintenance and should not be used for regular use (such as typing letters or drawing pictures) or for surfing on the Internet.

So that you don't have to start your first experience with GNU/Linux using the superuser account, some distributions ask you to set up an unprivileged user account. You will need to know the real name of the user, select a username, and then provide a password.

Next, you will need to create a boot disk. You'll need to get out a blank floppy disk for this step. Follow the instructions to create the boot disk and then label the disk something like "Linux-Mandrake 7.1 Boot Disk." It is very important that you create this disk. If the boot loader is not installed correctly, this disk will enable you to boot the operating system so that you can begin enjoying all that GNU/Linux has to offer.

The last step in this part of the installation process asks where you want to install the Linux boot loader, LILO. Linux-Mandrake makes a suggestion as to the location where LILO will be installed.

### New Term
A boot loader is a program that steps in just after the BIOS loads and offers you the opportunity to start one of a number of operating systems that might be installed on the computer. The boot loader that installs with Linux is LILO.

## Working with the X Window System

The end of the installation process is the most difficult, and the most important. It's time to set up your video card and monitor so that you can use the X Window System. You'll need it to use any of the graphical desktop environments, such as GNOME. If the video card and monitor are listed as compatible hardware for the GNU/Linux operating system, this process will be much easier.

You'll first be presented with a list of monitors. Search through the list to see whether your monitor is listed. If it isn't, you'll need to select one of the generic monitors. Pick the monitor that does what yours does. As in

```
A monitor that can do 1024 x 768 at 60hz
```

Next, you'll select a resolution and color depth for the display. It is very important that you do not exceed the capabilities for your monitor and video card.

After you enter the correct information, the installation process will ask whether you want to test the X configuration. Answer yes. You should see a message that says, Can you see this? If you can, select Yes. Don't worry: If you can't see the message, a few seconds will pass and it will be assumed that the test failed and you'll be sent back to the beginning to try again.

The last step in the X configuration process is to tell the system whether you want the system to start the X Window System automatically when the system boots. Click the No button. Should you have a problem, you would rather be at the shell prompt when the system starts. From the shell prompt, you need only type `startx` to display the graphical user interface.

Congratulations! You've made it to the end of the long installation process. Remove the floppy disk and the CD-ROM from the drives and let the system restart itself.

## Logging In and Logging Out

You can quit holding your breath. Take a look at your monitor; you should see a login prompt. What's a login prompt? To put it simply, the login prompt is where you type in a unique name that identifies you as an authorized user on the system. Depending on the distribution you installed and how you set up the X Window System, the login prompt might take various shapes and forms. If you installed Linux-Mandrake and elected not to start the X Window System when the system boots, the login prompt and associated bits of information might look as shown in Listing 2.3.

### LISTING 2.3 A Sample of the Linux-Mandrake Login Screen

```
Linux Version 2.2.15-0.25mdk
Compiled #1 Mon Apr 24 03:00:34 PDT 2000
One 133MHz Intel Pentium Processor, 80M RAM
264.60 Bogomips Total
localhost.localdomain

Linux Mandrake release 7.1b (hydrogen)
Kernel 2.2.15-0.25mdk on an i586 / tty1
localhost login:
```

That's a lot of information. And, yes folks, this is not the computer you saw in Listings 2.1 and 2.2. It is one of the other computers in our computer lab and the one you'll see most often as you flip through these pages. Listing 2.3 shows an old, beat-up computer with a 133MHz Pentium processor and 80MB of RAM. But, back to the important part, the login prompt, which is followed by the cursor. What does it mean to log in? Logging in involves supplying a username and a password, which Linux verifies to determine whether the user has the authority to access the computer system.

### New Term
When you installed and configured the Linux system, you set up at least one user account—the superuser account whose username is root. The superuser has unrestricted access to the entire operating system—every file and every command. Only the superuser can change the system setup and configuration. You might have also set up an unprivileged user account. This account is assigned to a regular user. Such a user can access files in his home directory and files used by general users (such as help files and program execution files).

At this point, you need to give the system your username before you can do anything with the system. The username that you supply is up to you. Every distribution requires that an account be created for a user named root. This account is assigned to the superuser (or the person in charge of maintaining and updating the computer system), and should be used only when performing system administration tasks.

### New Term
The system administrator is responsible for the care, maintenance, upgrade, repair, configuration, and security of a computer, the computer operating system, attached peripherals, installed applications, and data files. The system administrator grants access to the computer, peripherals, and files to the various users on the system. The system administrator also makes sure that the users do not have problems operating the system and that the system is configured to efficiently help them perform their jobs.

Your other option is to log in as an unprivileged user. You might or might not have been given the opportunity to set up this type of user account during the installation. If you did not set one up, turn to Hour 12, "Sharing Files with Other Users on the System," to
