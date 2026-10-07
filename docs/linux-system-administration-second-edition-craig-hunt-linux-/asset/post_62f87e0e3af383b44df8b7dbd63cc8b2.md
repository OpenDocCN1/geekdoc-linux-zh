
There are many other kernel parameters that might give you a performance gain. Since these are CPU–specific, we'll leave it to you to evaluate their potential benefit to your systems. Chapter 8 covers other kernel compilation options and procedures.

## Optimizing Applications

Just as the kernel code can be recompiled to optimize a computer system's performance, so also can the application code be optimized. If you download a tarball, read the documentation to see if there are system–specific optimizations that you might use. Most Linux software comes with an INSTALL file, which contains instructions for installation. Additionally, you'll likely find README files, which will tell you specific things to do for your operating system and/or hardware.

## Tuning the X Window System

The X Window System, the subject of Chapter 13, is a critical part of a desktop system, since it provides the user a GUI environment in which to work. Users like graphical tools, and some Linux administrative functions are so complicated that the ability to perform them without graphical tools is all but forgotten. Network configuration, for example, is almost exclusively done via some graphical tool like neat or kppp. It's certainly possible to configure a network by editing the scripts, but fewer and fewer administrators do it that way anymore. As a result, most of the desktop systems you administer and probably many of the servers will be configured to run X even though some distributions don't install X on servers by default. X is quite resource–intensive, though. Anything you can do to tune X is a good thing.

## Window Managers and Integrated Desktop Environments

Window managers and integrated desktop environments (IDEs) can really chew up memory and CPU cycles. First, since it seems to be a source of confusion even for seasoned system administrators, you need to understand the difference between the two. A *window manager* is the interface between X and the user. It is the mechanism by which the user can move, resize, and otherwise manipulate the windows that X gives it. Some of these window managers have task bars, virtual desktops, file managers, and theme association; others do not. An integrated desktop environment brings some inter–application consistency and additional tools to this environment. It provides things like a file browser and user desktop, along with assorted minor tools and utilities, and it influences the overall look and feel of the environment. An IDE comes with a specific window manager but may be used with a different window manager if that manager is IDE–aware. We covered the specifics in Chapter 13 where we discussed X in more depth, but the essential point is that an IDE runs atop a window manager. If you need to reduce overhead, you can get rid of the IDE, which will free up a lot of resources.

If you do that and are still not getting the performance you need (but still need the X environment), try changing window managers. If you're looking for performance instead of "pretty," try the Tab window manager (twm). This environment provides title bars, icon management, point–and–click, and other functions, but it does so with line art instead of using the high–overhead 3D effects or shading. The switch to twm will buy you some performance improvement.

## Removing Bad Modes from XF86Config

Another X performance issue involves the startup process, which although faster than Microsoft Windows, is much slower than it should be. What could make it go faster? If you watch the output of the startx command (press Shift+Alt+F1 to go back and look), you'll see many lines similar to this:

```
(--)
SVGA: NM2160: Removing mode (640x400) that won't display properly on LCD
```

This line represents a video mode that was looked at and determined not to fall within the capabilities of your video card/monitor combination. Each time X is started, the system reevaluates these modes. One way to speed things up a bit is to remove any bad video modes from your XF86Config file. The mode line will look like this:

```
Modeline  "640x400"  31.50  640  672  736  832  400  401  404  445  -
    hsync  -vsync
```

Simply comment it out by placing a # symbol in front of the word Modeline. The next time X is started, these modes won't be attempted, saving you a little time for each mode deleted. This will not improve performance once X is running, however. If you are looking for performance instead of quality graphics, remember that lower resolutions run faster.

## Upgrading

"When should I upgrade my operating system?" is a question that plagues many system administrators. Do you upgrade simply because a newer version has come out? Do you upgrade individual packages whenever there is a bug fix? Do you reinstall from scratch or perform the distribution's upgrade?

It's usually best to back up the system, reinstall, and then dump configuration files and user files over the new system. This may cause you some trepidation at first, since you won't be sure that you remembered to put all the configuration data back; you may think you will overlook something. If you use the installation process's upgrade facility, you'll probably never have a problem with it. As you became more confident, however, you'll probably decide that you don't like having residue from the previous version mixed in with the new version, so you'll begin backing up the system, and doing a full install.

You should not blindly upgrade or reinstall a working, configured system just because a new version of the operating system has come out. The distribution's Web site will contain detailed information about what prompted the new version and what has been upgraded. Read those notes and do a cost–benefit analysis. Is the gain worth the time? Are there risks if you don't upgrade, and do these risks apply in your setting? Perform an upgrade if the new version offers several significant security fixes or a major change in overall kernel philosophy. If there are only a few security fixes, you can upgrade those packages only, and leave the rest alone. You'll get more comfortable with what requires an upgrade as you progress.

## In Sum

A computer's performance can be influenced by many factors, both hardware and software. If your system isn't performing to your liking, you might try upgrading your hardware, but devoting some time to optimizing your computer may save you the cost of hardware upgrades. Indeed, some hardware upgrades won't do much good unless accompanied by appropriate software tuning. Enabling 32-bit DMA transfers on IDE hard disks is one such case. You can also tune your computer's use of the hard disk, of memory, and of the CPU by appropriate configuration options. Some optimizations (particularly for the CPU) require you to recompile software for your system, or at least to locate software compiled with better–than–386 optimizations.

In Chapter 17, "Making Your Job Easier with Scripts," we'll try to save you some time each day by exploring how to automate some of the more mundane tasks. Since you know how, you can spend the extra time tweaking your systems to gain optimal performance.

## Chapter 17: Making Your Job Easier with Scripts

### Overview

A well-written script can be a system administrator's best friend at times when there is much to be done and not enough hands to do it. Large, repetitive tasks are especially easy to script—and especially tedious to perform if you don't. As you get accustomed to scripting, you'll discover many more uses for it. You'll find yourself writing scripts even to perform the smaller tasks.

This chapter begins with and focuses most strongly upon the Bash shell scripting language, but there are several other types of scripts, including Bourne shell scripts, Perl language scripts, Python language scripts, awk scripts, and sed scripts. Even more variations are in use, but these seem to be the most popular among Linux system administrators today. This chapter touches upon each of these script types, and also covers system initialization scripts and scheduling scripts to run at times of your choosing.

Determining which type of script to use is a tricky process. Since the role of a script is to perform some lengthy task quickly and efficiently, system administrators often simply use what they know best. Bash shell scripts are quite common. Bourne shell scripts are popular too since they are compatible with the Bash shell and add the ability to use them with the Bourne shell as well. Perl and Python are used frequently and are the favorites for CGI programming in support of Web site development. These two are really not well suited to anything that requires real-time response or multithreading. However. Of the two, Python scales better and is easier to read and understand. For more information, look at http://www.perl.com/ and http://www.python.org/. Although still used and maintained, scripts written in the awk text processing tool and the sed stream editor have very specialized uses and seem to be falling out of favor as new scripting tools are developed. (Java and Tcl/Tk scripts are not included in this discussion because neither seems to see significant use as a system administration tool within the Linux world.)

**Note**
Shell scripts are actually computer programs. They differ from most programs, however, in that they're written in *interpreted* languages—that is, languages that are interpreted directly from human-readable form rather than first being converted into machine code by a compiler. This makes shell scripts slower to execute than their compiled brethren, but the same fundamental principles apply to all programming languages. Because of the complexity of any programming language, this chapter cannot provide a complete description of even a single scripting language, but it will provide a quick introduction to get you on your way to writing your own scripts or modifying existing ones.

### Common Scripting Features

No matter what the scripting language, there are certain common features you should understand. Most of these features are common not just to scripting languages, but to compiled languages as well. These features do take slightly different forms in different languages, however. For instance, each language has its own rules for identifying variables, and equivalent commands can be represented by different words in different languages, much as words with the same meaning are different in different human languages. It's important before proceeding further that you understand some of these fundamental features of programming languages.
