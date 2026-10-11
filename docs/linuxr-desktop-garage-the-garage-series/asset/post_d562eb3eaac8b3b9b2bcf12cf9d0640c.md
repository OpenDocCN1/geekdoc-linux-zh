
## Keyboard

This option is for setting the language of your keyboard.

## Language

Here you can set the default language for your system. If you are missing a language that you would like to have available, you can grab your install CDs and add it from the many languages available.

## Login Screen

We were here in the last chapter, remember? Ah, the memories. Anyway, this is the dialog box where you can change the settings for the GDM login manager program.

## Network

The settings in the Network Configuration dialog box are for changing the settings on your network card and your computer’s network identification information. Descriptions are at the top of each tab.

## Printing

You can add and edit printers with the Printer Configuration Tool. We talk more about printing in a bit.

## Red Hat Network Configuration

If you choose to use the Red Hat Network for your updates, this dialog box sets the addresses used, lets you adjust settings for controlling package management, and choose exceptions.

## Root Password

Change the root user’s password from here.

## Security Level

This dialog box is for setting your firewall options. If you enable the firewall, you can check boxes for which services and devices are allowed. Using the firewall is an excellent idea for broadband connection users at home.

## Sound Card Detection

The only thing you can really do here is listen to that “if Zmdir played the guitar” sound and then answer Yes or No for whether you heard it. I suppose it’s a good tool to make sure your sound card is working, but I can think of more fun ways.

## Users and Groups

Add and edit users and groups with this tool. You can create groups to use for setting permissions for more than one user at a time or create a class of users.

## System Tools Menu

Many of the entries in the System Tools menu deal with the hardware in your system. Other options are for some of the same things as the System Settings menu. Most of these tools are new, graphical ways to perform actions that previously could be done only on the command line. A majority of these tools require your root password.

## More System Tools

Poof! It’s empty? Well, if you haven’t installed KDE along with GNOME, then, yeah, this submenu is an empty placeholder for most default Fedora users. If you have installed KDE, two of the KDE disk utilities are listed here.

## Archive Manager

This option opens the File Roller program. File Roller is the same program that pops up when you double-click an archive (.zip, .tar, .gz, and so on) in the Nautilus file manager. It is a manager program for creating and extracting compressed files.

## Configuration Editor

This is the behemoth of controversy for many Linux GNOME geeks. The GNOME Configuration Editor (GConf, shown in Figure 3.2) is a GUI front end to editing a database of application preferences. People who hate it usually say that it is too analogous to the Windows Registry. People who like GConf enjoy the convenience of having all those settings in one place. People who are me think that you should not even touch any settings in this program unless you know what you’re doing and are confident in any changes you might make in there. However, poking around and taking a look is always encouraged.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_102_0.png)

**Figure 3.2**
The loved and hated GNOME Configuration Editor.

## Disk Management

With this tool, you can mount and unmount file systems on your computer, such as disk partitions and removable media such as CDs and floppy disks. You can also manage disks by right-clicking your desktop and choosing Disks from the pop-up menu.

## Floppy Formatter

I know, who uses floppies anymore? Talking about floppies is like hearing your uncle talk about those great eight-track tapes he used to have of the Doobie Brothers. If you still have floppies, well, here’s a tool to format them for you. The interface is very easy to use and gives you options for density and file system type so you can format floppies for use in other OSs.

## Hardware Browser

Take a look at what hardware is installed on your system in this tool. This isn’t the place to make changes to anything, but the Hardware Browser is the place to come when you need to know the brand or model of a device and don’t want to open the computer to find out.

## Internet Configuration Wizard

This wizard is magical. The Internet Configuration Wizard isn’t magical, but how can you expect me to resist saying that when they keep calling these things “wizards”? I’m a genius, but I’m only human. Here is where you can set up your Internet connection, whether it is a dial-up, broadband, wireless, or other connection.

## A Lesson to Learn

Seemingly illogical problems always crop up when using computers. There is a lesson to learn if you want to keep your sanity. Got a problem? Go around it. When you start to have a problem on a computer, you are tempted to find the exact problem and why you are having that problem. Something inside you tells you to fight it out. Fighting the problem takes a long time and can breed frustration. Often with computers, the best course of action is to find an alternative way to do what you are trying to do. Go around the problem. Then, if you feel the need, you can try to find out the cause and slay the issue later, when you are not in the midst of frustration.

## Kickstart

This tool writes a Kickstart file. A Kickstart file is a long, complex text file used to save installation settings for performing multiple Fedora installs automatically. Most desktop users will not need this.

## Network Device Control

The Network Device Control module is a tool for monitoring, activating, and deactivating hardware such as network cards and modems. You can also access the configuration of listed devices.

## Print Manager

After you add a printer, you might want to see what it's doing; you have the Print Manager to look at documents and status of the printer queue.

## Printing Notification Icon

This puts an icon in your system tray that you can click when you are printing to check the status of the print job.

## Red Hat Network

This brings up the dialog box for the Red Hat Network. This tool checks which system packages are available for update. You can use the Red Hat Network to keep your system up-to-date.

## Red Hat Network Alert Icon

If you haven't gotten rid of it yet, you probably have a round icon in your system tray for the Red Hat Network. This menu option puts the icon back if you remove it.

## System Logs

Log files are lists of events and warnings. This is a tool to view the log files for your system without having to use the terminal. Logs can be helpful for troubleshooting problems but don’t make for very interesting reading.

## System Monitor

You can view the current memory usage, processor usage, and running processes in the System Monitor. Some people like to incessantly stay abreast of their computer’s performance and keep this open all the time.

## Terminal

It’s the terminal. It’s your access to the command line. It’s your friend. Don’t be afraid of it. Open it. Like it. We have more brainwashing later to make you like the terminal.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_104_0.png)

### TOOL KIT 3.3: How to Do "Important" Stuff in Fedora

Now that you know what all those cryptic entries in the System menus are for, let’s get down to the nitty gritty. When you have something boring to do that can be called maintenance or a utility, you usually don’t feel like wasting time figuring out how to get it done. Here are a few common utility tasks you might need to know how to do.

- Change Your Password
  Main menu > Preferences > Password
- Change the Root Password
  Main menu > System Settings > Root Password
- Manage Users and Groups
  Main menu > System Settings > Users and Groups
- Change the Date and Time
  Main menu > System Settings > Date & Time
- Mount Disk Partitions and File Systems
  Main menu > System Tools > Disk Management
- Start or Stop a Service
  Main menu > System Settings > Server Settings > Services
- Read the Logs
  Main menu > System Tools > System Logs

**BIG BROTHER CAN BE PRETTIER**
If you keep the System Monitor open often to spy on your computer’s performance, you can spy in more style than with the GNOME tool. A program called Gkrellm (http://www.gkreliim.net/) is

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_104_1.png)

**UNDER THE HOOD**
