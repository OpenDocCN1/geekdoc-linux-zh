
![](img/12d790664598bbf390261087fbe55bbc_139_0.png)

**Figure 6.17:** The fourth tab of the Login Manager.

As you can see, the first two settings allow you to determine what users can use the console/shell and what users can log on remotely. The second set of options, Commands, determines what happens when you halt or reboot. You should leave these with the default settings unless you have some very compelling reason to alter them. The third section simply determines whether or not to show the boot options on the login screen. This will make very little difference unless your machine is set to dual boot with two or more alternative operating systems (such as Linux and Windows).

The fourth section is the most interesting. Here is where you decide what startup options the user has. You will note that under Available Types there are four different settings for the user interface. As was mentioned earlier, while KDE and GNOME are the most popular graphical user interfaces, they are not the only ones available for Linux.

The Users tab allows you to select an image to display and to choose whether or not to show a list of users for the person to pick from. This would mean that instead of simply typing in their usernames and passwords, they could pick from a list of users and then enter the appropriate password.

This sixth and final tab, labeled Convenience, allows you to set some items that you may find convenient. However, you should remember that convenience almost always comes at a price. On this screen you can choose to allow people to log on without a password. Unless the machine is a home machine, such an option would be very foolish. Even if it is a home machine, you should think very hard before choosing this option. Do you really want your 10-year-old to be able to log on as root and have complete system administration privileges?

## Regional and Accessibility

This section allows you to set some accessibility options, which we have examined previously. However, it also allows you to reconfigure your machine for a given region. After you have chosen Regional & Accessibility, click on Country/Region & Language, and you should see a screen much like that in Figure 6.18.

![](img/12d790664598bbf390261087fbe55bbc_140_0.png)

**Figure 6.18:** Country/Region & Language.

The first tab, Locale, allows you to set what nation and language settings to use. You can see at the bottom of this tab that your current settings are shown. The second tab determines how you will display numbers. The third tab is probably the most important for setting up your machine for a different country. This tab allows you to change how money is displayed. Obviously, currency is quite different from one nation to the next, so this tab can be quite important. The fourth tab establishes how you will display times and dates. This tab is more a matter of preference than regions. The final tab will allow you to choose paper format and measurement systems. If you are traveling abroad, you should remember that most countries use the metric system.

## Scheduling Tasks

One very useful feature of Linux is the capability to schedule certain tasks to take place at some future date and time. If you will recall, earlier we discussed programs that run in the background and accomplish tasks. In Linux and Unix these are referred to as daemons, and in Windows they are called services. Most daemons in Linux end in a letter d. The daemon that is responsible for handling scheduled tasks is called crond, for chronological daemon. You can completely manage crond via shell commands, and we will visit that topic in Chapter 8, “Moving from Microsoft Word to Open Office,” but right now we will see how to do this through the KDE interface. Like most tasks, scheduling tasks via the KDE interface is a lot easier and more user friendly than doing it via shell commands. To get to the Task Scheduler, you can go to System Tools and select Task Scheduler. You should see something much like what is displayed in Figure 6.19.

![](img/12d790664598bbf390261087fbe55bbc_141_0.png)

**Figure 6.19:** The Task Scheduler.

To schedule a new task, you simply expand the category appropriate to your task and right-click on New Tasks, as shown in Figure 6.20.

![](img/12d790664598bbf390261087fbe55bbc_141_1.png)

**Figure 6.20:** New Tasks.

When you do this you will see a screen like the one shown in Figure 6.21. On this screen you can decide when you want this task to run. You can pick months, days, time of day, even down to the exact minute when you want the task to run. Then use the Browse button to select the program you want to run.

![](img/12d790664598bbf390261087fbe55bbc_142_0.png)

**Figure 6.21:** Scheduling a new task.

That is all that is required to schedule any task. You can have any program you want run automatically at a certain time and date. This is very useful for system administrators who want particular programs or scripts to run when they are away. This allows you to have certain cumbersome administrative tasks take place when you are away from the computer.

## Kickstart Configurator

Linux, being a descendent of Unix, was designed with a powerful high-end server in mind. For that reason, Linux, like many Unix variants, comes with a wide assortment of configuration utilities. Some of these, such as the System Monitor, have Windows analogs you can relate to. However, some utilities, such as Kickstart Configurator, do not have any close analog in the Windows world. The Kickstart Configurator is a very useful KDE program. It is found under System Tools, and the main screen is shown in Figure 6.22. The Red Hat official documentation describes Kickstart in this manner: “Kickstart Configurator allows you to create a kickstart file using a graphical user interface, so that you do not have to remember the correct syntax of the file.” This means it allows you to generate a configuration script via a very easy to use graphical interface. It allows you to reconfigure all the things you set up in Chapter 2. It is often used by system administrators to create a single install script to be used for installs across an organization. From the basic configuration screen, you can change the language, mouse, keyboard, time zone, and other important settings.

![](img/12d790664598bbf390261087fbe55bbc_143_0.png)

The next screen that is of particular interest to us is the Boot Loader Options screen, shown in Figure 6.23. As you can see, this screen allows you to choose which boot loader to use. Even though GRUB is the newest boot loader, you don’t have to use it. You can use LILO if you so desire. You can also choose to have a password on GRUB if you like.

![](img/12d790664598bbf390261087fbe55bbc_144_0.png)

**Figure 6.23:** The Boot Loader Options screen.

After that, you come next to the Partition Information screen, shown in Figure 6.24. This screen should be used with great caution. You can readily see that one option is to remove all existing partitions. If you select this, you would wipe out your entire hard drive. This screen is of use only in certain restricted cases. For the most part, you will want to avoid altering anything on this screen.

![](img/12d790664598bbf390261087fbe55bbc_144_1.png)

**Figure 6.24:** The Partition Information screen.

The next two screens, Network Configuration and Authentication, provide yet another way to configure options we have already explored. We have seen three different ways to configure your network card after installation. Also recall from our earlier discussion of authentication that, if you lack any substantial familiarity with security, you should probably leave the authentication at default settings.

The Firewall Configuration screen, like the two preceding screens, provides yet another way to configure a particular part of your system. We mentioned firewall configuration during the initial install and noted that you could always reconfigure the firewall settings at a later date, as you learned more about networks. The Kickstart Configurator is one of the vehicles you can use to reconfigure your firewall.

The X Configuration screen, shown in Figure 6.25, is quite interesting. With this screen you can reconfigure your system’s screen resolution, video card, monitor, and default desktop. This screen is likely to be of interest even to casual users. One setting that people on any system (Windows, Macintosh, or Linux) seem inclined to change from time to time is their display settings.

![](img/12d790664598bbf390261087fbe55bbc_145_0.png)

The final three sections of Kickstart Configurator are used only to alter how an installation proceeds. Since we have already installed, these particular settings are not important to us at this time. If at some later date you want to install a new version of Red Hat, you can follow the installation instructions.
