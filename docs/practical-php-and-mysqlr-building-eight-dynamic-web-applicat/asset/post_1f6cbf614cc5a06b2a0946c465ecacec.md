
# CHAPTER 3
# Running the Projects

This book is crammed full of projects, lots of delightfully delicious projects that show you how to do interesting things with PHP and MySQL. Within each project are pages and pages of source code that gradually build up each project. Although you are more than welcome to sit there and carefully type each line as you go, we figured you might want to just run the projects right away and see how they work. Sound good? Well, you will be pleased to see that the shiny disc wedged into the book provides you with hours of project-running enjoyment!

So what is on the disc? Well, the disc is called a Live CD, and it provides you with a simple and easy means of running a complete operating system on your computer without touching your existing hard disk in any way. The way it works is that you pop the disc in the drive and boot from it. The computer then pretends that the CD is a hard disk and runs the operating system like any other. This means that you can play around with the system as much as you like, and it won't touch your precious hard drive. Cool, huh?

## ABOUT THE DISC

With most programming books, you often get a disc that contains the code from the book. This handy supplement saves hours of laborious copying of code from the book to your computer. Despite saving hours of typing, the code-on-the-disc approach still makes the assumption that you actually have the software required to run it. As such, if you know you want to learn something (such as PHP and MySQL), but you don't have the PHP and MySQL software to run the code, you are stumped.

Not so with this book. The Live CD not only contains the code for each of the projects, but also includes a complete development environment in which to run the code. You get PHP and MySQL, as well as Apache, phpMyAdmin, Mozilla Firefox, PEAR modules, and much more—all neatly contained on the Linux operating system.

Now, we know what we are thinking—“Oh, I need to go out and buy a new hard disk, or I need to partition my existing disk, or I need to…” Relax. There is no need to buy a new hard disk, no need to partition, and no need to worry. The entire system runs from the CD.

## Live CDs: A New Approach

In recent years, the Live CD has really taken off. The idea is simple: You take an operating system (usually Linux), and instead of running it from a hard drive, you run it from a CD or DVD. This provides a number of benefits. First, you can try out an operating system without actually installing it. When you run the disc included with this book, it won’t ever touch your hard drive. Because the system runs from the CD, you can play around with it, break things, and experiment. Not only is your hard drive completely safe, but you can also reboot the CD to get the original system back at any time. Second, a Live CD provides a great way to “take your system” with you; just put the disc in a drive of any computer and reboot to run it.

## Starting the System

Not all computers automatically attempt to boot from the CD/DVD drive when starting. If you turn on your computer and see the CD/DVD drive light flicker, the computer is looking for something to boot. In this case, put the Live CD in and reboot to get started!

If the light did not flicker, you may need to enable booting from the CD/DVD drive in your computer’s BIOS. To access the BIOS setup, your computer will have a particular key or key combination to press to enter it. Common keys are F12 and Del. I recommend that you refer to the manual for your computer or motherboard to find out how to boot from the CD/DVD drive.

For best results, find a computer that has lots of RAM. Because a Live CD is a read-only medium, areas that need to be written to for running the Linux system are stored in RAM. So, for example, the live CD will boot faster and run better on a computer with 1GB or more of RAM than it will on a computer with 256MB of RAM.

When your system is enabled to boot, pop the disc in the drive and reboot. After a few seconds, the screen shown in Figure 3-1 should appear.

![](img/c75d0c4fa51711b62f211459ae794f3f_69_0.png)

**FIGURE 3-1** The bootup splash screen, lovingly customized for the book!

Press Enter to start the system. Soon, you’ll see the desktop boot and the splash screen appear, as shown in Figure 3-2.

![](img/c75d0c4fa51711b62f211459ae794f3f_69_1.png)

**FIGURE 3-2** The desktop loading

Finally, double-click the Start XAMPP icon. XAMPP starts in a terminal window, as shown in Figure 3-3.

![](img/c75d0c4fa51711b62f211459ae794f3f_70_0.png)

**FIGURE 3-3** Firing up XAMPP

## RUNNING THE APPLICATIONS

Running the different applications included with the disc is simple—just double-click one of the icons on the desktop to access that particular application. When you double-click an application icon, Firefox opens and displays the application that icon represents in the window. As an example, double-clicking the Forums icon causes the Forums application to appear, as shown in Figure 3-4.

If you want to play with the source code to the applications, double-click the Bluefish icon. When it loads, use the side panel to load the project that you want to develop. Remember, all projects are stored in /opt/lampp/htdocs/sites, so be sure to choose the right project inside that directory. Later, you can run the code from those project directories by entering http://localhost/sites in the location box of your Web browser on your Live CD.

![](img/c75d0c4fa51711b62f211459ae794f3f_71_0.png)

**FIGURE 3-4** Loading an application is as simple as double-clicking an icon.

### USING XAMPP

Other than the operating system included on the Live CD, the most critical piece of software is XAMPP. The XAMPP project provides the core pieces of software required for LAMP development (Apache, MySQL, and PHP) in a single download-able archive. As such, you can go to the XAMPP Web site (http://www.xampp.org), download the latest version to your computer, unzip it, and run it; you now have a complete LAMP system set up to do your development. This saves the hours of tweaking and configuration and frustration with the non-trivial installation of the separate Apache, MySQL, and PHP components.

Not only does XAMPP ease the installation of these components, but it also includes a huge array of additional software, including phpMyAdmin (used to create databases easily), PEAR modules (additional features in PHP), graphics libraries, documentation, and much more. XAMPP really does provide a comprehensive and complete Web development platform.

Although you can just boot from the Live CD, start XAMPP, and access your applications straight away in the Web browser, it will be useful to have a look at some of the common features of XAMPP. The following sections cover these features, so you can get to know the system.

> **NOTE**
>
> **Running XAMPP Elsewhere?**
>
> If you want to run the XAMPP included on the disc on a different operating system, you can find a file called *laminp.tgz* in `/opt`. Just copy that file to a Linux system, unzip it, and then run `/opt/laminp/laminp`, as shown in the following “Starting and Stopping” section.

## Starting and Stopping

XAMPP installations in Linux are always installed to the `/opt` directory. Inside the XAMPP directory is the `laminp` command, which can be used to start and stop the XAMPP system. To start XAMPP, run the following command:

```
`foo@bar : /opt/laminp $ sudo /opt/laminp/laminp start`
```

Because XAMPP provides system services, you need to be the super-user to run the command, the reason for using `sudo`. You can also stop XAMPP by using the following:

```
`foo@bar : /opt/laminp $ sudo /opt/laminp/laminp stop`
```

You can stop and start XAMPP by using `restart` (this is the command that the Start XAMPP icon on the desktop runs):

```
`foo@bar : /opt/laminp $ sudo /opt/laminp/laminp restart`
```

This command actually has a huge range of features available, and you can see them all by running the command without any options:

```
`foo@bar : /opt/laminp $ sudo /opt/laminp/laminp`
```

Table 3-1 provides a list of some of the commands that may be of particular interest for starting and stopping specific components.

When the XAMPP system is started, you can use the Web browser to view the running server by visiting `http://localhost`. When you visit that page, you will see a number of included Web pages that are part of the XAMPP system. These pages provide a number of small example applications, links to other parts of the system, and information about the running.
