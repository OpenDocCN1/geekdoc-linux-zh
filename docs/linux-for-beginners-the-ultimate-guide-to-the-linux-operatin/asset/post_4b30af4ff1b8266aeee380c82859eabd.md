
chapter, so go ahead and choose the version that you want to work with. Also, if you notice on the right hand side, it will ask you to choose your flavor of that particular version. This is them asking you whether you want to 32-bit or the 64-bit version of the Ubuntu Linux desktop. Just choose the version that applies to your system and then click “Download.”

![](img/38783e2b6fd4fbccebb177aa2953d843_41_0.png)

Go ahead and wait until ISO file download is finished. Once that's done, burn that ISO file to a CD or DVD, put that into the system where you want to install Linux, and then boot off of it. Now we'll proceed with the installation process.

The interesting part that you will probably notice during the desktop version's installation is that it will give you two options: try Ubuntu or install Ubuntu. The curious thing about Linux is that they have things called Live CDs. What a Live CD means is that the entire operating system is installed and can be run off of the CD. When you are dealing with Windows, Mac OS, or even Linux server, you always have to install the operating system for it to work on the computer. With a Live CD, you can actually boot straight off of the CD and use all of the functionality of the operating system without installing it. You can surf the web, manage files, edit text, etc. by just running the entire operating system from the CD itself.

In addition, if you have a Windows computer, you can put in a Linux Live CD, boot from it, and do whatever you want to do with it without affecting the computer at all. This is a great way for a user to test a particular Linux distribution first without going through the lengthy installation process.

So, going back to our installation process, just go ahead and click install Ubuntu for now.

![](img/38783e2b6fd4fbccebb177aa2953d843_42_0.png)

Next, you will be asked to choose your region and time zone. Go ahead and choose the region and time zone that applies to you and click “Forward.”

![](img/38783e2b6fd4fbccebb177aa2953d843_42_1.png)

Again, just like in the server edition, the installation will now ask you to choose your keyboard layout. Go ahead and choose the one that applies to you and click “Forward.”

![](img/38783e2b6fd4fbccebb177aa2953d843_42_2.png)

Next, the installation will ask you to prepare the disk space in your hard drive prior to installation. If you want to use your entire disk for Ubuntu alone, go ahead and choose the option that says, “Erase and use the entire disk.” However, if you have another operating system on your hard drive and you want to install Linux inside a different disk partition, then choose the option that says, “Specify partitions manually.”

Specifying partitions manually involves telling the installation process how much disk space you want to allocate for the Linux installation. For now, since you are still a beginner, let us assume that you are just installing Linux alone in your hard drive, and that you are not going to do any partitioning. So go ahead and choose, “Erase and use the entire disk” and press forward.

![](img/38783e2b6fd4fbccebb177aa2953d843_43_0.png)

After you press “Forward,” the installation will ask you what your name is, what name you want to use to log in, the password that you want to put for the user account, and the name you want to give the Linux computer.

![](img/38783e2b6fd4fbccebb177aa2953d843_43_1.png)

Also, if you scroll down a little bit, you will see that the installation is asking you whether you want to log into the computer automatically once it boots up, require a password during log in, and require a password during login and decrypt your home folder. The latter option only applies if you installed Linux with the encryption feature enabled.

Go ahead and enter the information needed and then press “Forward.” Next, the installation process will show you the all the settings and options you have chosen so far and what it is about to do. If everything looks okay, go ahead and press “Install.”

![](img/38783e2b6fd4fbccebb177aa2953d843_44_0.png)

Once you click install, the installation will now proceed and you will see a window that has a progress bar at the bottom. At this point, just exercise patience and wait until the progress bar reaches 100%.

![](img/38783e2b6fd4fbccebb177aa2953d843_44_1.png)

Once the progress bar reaches 100%, it will tell you that the installation is complete and that you need to restart your computer to finalize and use the new installation. Go ahead and click “Restart Now.”

![](img/38783e2b6fd4fbccebb177aa2953d843_45_0.png)

Again, the actual time that it will take for the process to finish will depend on your hardware. Do realize you should look at the hardware requirements for the desktop version of the Ubuntu Linux operating system. Remember, the server version is extremely stripped down. There is almost nothing to it really.

The desktop version has all these fancy graphics and user interfaces, as you can evidently see even from the installation itself. Where the installation of the server version basically is text based, the installation for the desktop version actually has graphical user interface windows and option buttons that you can actually click on.

All of these fancy graphical niceties actually does require pretty decent hardware. It is therefore recommended that if you are going to use the desktop version of Ubuntu Linux, your computer should be at least five years or younger with at least 1 Gigabyte of RAM. If you have any less than that, it may not have the resources it requires to run.

But in the grander scope of things, the desktop version of Linux still has a much lighter system requirement compared to Microsoft Windows or Mac OS.

After the restart sequence of your computer is done and you finish logging into Linux using the credentials that you entered during installation, you will now reach the desktop of Ubuntu Linux.

![](img/38783e2b6fd4fbccebb177aa2953d843_46_0.png)

Just like what we have mentioned prior, you now have something that vaguely looks like Microsoft Windows or the Mac OS operating system. As you can see right off the bat, you have your applications on the left hand side such as Firefox for web browsing, OpenOffice Suite for word processing tasks, your home folder, Linux settings, Amazon, and much, much more.

So, that is the Ubuntu Linux desktop version.

## Chapter 4: Basic Linux Tasks/Commands

In this chapter, we are going to go over the basic tasks that you can perform in Linux. We are going to show you how to install applications, how to update applications, how to look at the Linux task manager and even terminate processes if necessary, how to start services, and a whole lot more. These are the basic tasks that you will need to understand in order to do anything else in Linux.

Everything that will be shown here will be on the Ubuntu Linux server version. This is not the desktop version. You are going to be looking at the LUI, or the line user interface. You will be typing in commands on the keyboard instead of clicking a bunch of options in a graphical user interface.

While this may seem a little daunting and tedious, keep in mind that in Linux, all types of serious administration have to be done at the command line. This is an operating system developed by programmers for programmers primarily after all.

Even if you are using the desktop version of Ubuntu Linux, it does not give you the full power of the operating system unless you use the terminal or command line to execute certain tasks. A lot of times, even if you are using a desktop version, you still have to open up a terminal screen and type out all the commands that you need to type out to administer the system.

### Sudo

The first command that we need to talk about before you start doing any of the other commands is "sudo." Sudo basically means "super user." In the previous chapters, we discussed how different distributions do things slightly differently, and that every single distribution of Linux has its own quirks; its own little ways of doing things depending on what the creators are worried about.

One of the things that the creators of Ubuntu Linux were worried about was security. As what we talked about before, in every Linux computer, there is a user called Root. Root is the highest level user on the computer. It is kind of like the administrator in a Microsoft Windows computer.

Just like on a Windows computer, if somebody logged in as the administrator, or somebody logged in as root on Linux, they can do absolutely anything they want to that computer. They can install viruses, malware, or spyware, or basically just cause a lot of havoc. Hackers, using special programs and scripts, can also try to login as Root and cause all these problems.

To alleviate the possibility of a hacker obtaining root access, the Ubuntu creators decided they never want anybody to login straight as Root. So in Ubuntu Linux, you cannot login as the user Root.

Now, here comes the problem. Since you cannot login as Root, how do you do all these administrative tasks then? How do you execute administrative processes? What they have is this program called sudo. It is basically a command prefix that tells the operating system that you want to run a particular process as the super user or root.

Sudo temporarily gives a user administrative access—root access—to execute an essential command in Linux. In the Windows operating system, sudo is the equivalent of the "Run as Administrator" option each time you want to run a program with administrative rights in Windows.
