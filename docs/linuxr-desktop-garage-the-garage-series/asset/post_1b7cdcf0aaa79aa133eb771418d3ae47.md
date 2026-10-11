
## Mandrakelinux Control Center

Trying to say whether the menu arrangement of Fedora's system utilities or the control center cluttering of Mandrake's is better just comes down to small details and opinions. Both give you convenient access to system settings and tools. The Mandrakelinux Control Center might be a bit more convenient for some people because everything is in one place for you. It does, however, take a few extra clicks to get to the tools.

When you open the Control Center, you are attacked by giant icons. Maybe they don't attack you, but they are pretty big. The Control Center is arranged into categories with modules that could be called either settings or tools all mixed into their respective categories. Not only are the categories smartly named and arranged, but most modules give you a quick introductory description when you open them. All that attention to information and usability makes dealing with mundane system tasks in Mandrake quite easy.

Open the Mandrakelinux Control Center by going to main menu > System > Configuration > Configure Your Computer (see Figure 3.3). You will need your root password. Let's go over what cereal box toy surprises lie underneath each of those giant icons.

Figure 3.3
The Mandrakelinux Control Center.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_105_0.png)

the Linux geek's Swiss army knife, with system monitors, mail notification, and more. You can even choose skins for the program to make it pretty.

### Boot

All the modules in the Boot category pertain to what happens when you turn on and log into your computer. The Autologin module asks whether you want Mandrake to skip the login manager and start your desktop for you. Autologin is okay if you don't have others around your computer who shouldn't be messing with your programs and data. The Boot Loader module opens settings for the boot loader program, usually LILO or Grub. Unless you need to change options because you are dual-booting, you can probably leave these settings alone. Boot Theme lets you add a theme to the boot screen.

### Hardware

Yep, this is where you can set up all the hardware connected to your computer, or at least most of it. The Hardware module is a browser to get information about the various cards, input devices, ports, and doodads in your system. As you click each device in the list, configuration modules or tools show whether they are available. Other modules in the Hardware category include settings for Monitor, Screen Resolution, Keyboard, Mouse, TV Card, and Scanners, which are all easy to understand. The Graphical Server module gives you display settings for the X server, such as monitor and graphic card. The Printers module lets you add printers. We go over printing in more detail later.

> **Mounting Files, Not Horses**
> 
> Mounting and unmounting file systems can be a strange concept for many new Linux users. Let's compare file systems to books. You might have a book sitting by you. You might even be touching that book, but you can't read it until you open it. To read and write to a file system, Linux needs to open it first, which is expressed in the kooky language of commands as mounting a file system. Other operating systems mount and unmount file systems as well, but they hide it. No hiding in Linux, no secrets. Linux will let you see the inner workings of the OS. Many utilities are in your distro and desktop environment that mount file systems automatically for you, but there's no harm in learning about what is going on under the hood.

### Mount Points

Most users will not need to change the options in these modules. The Partition module brings up the same partition tool that you used during install. You can change the partition table for your computer, but it's not a good idea. If you really messed up on the partitions, you might want to just reinstall to have a clean start. You can change the options for each type of removable media (such as CDs and floppies). NFS and Samba mount points are shares on your local network, including Mac and Windows shares, that use the same protocol.

Samba is the most common of the two protocols. WebDAV Mount Points gives you options for connecting to a remote Web server. Local Disk Sharing is where you can set up directories on your computer to share with others on your local area network.

### Network & Internet

This module gives you options for managing various types of connections. In addition, you can share your Internet connection with other computers on your network and edit proxy settings. You will use some of these modules in a bit to set up an Internet connection.

### Security

The three modules in this category make the paranoid among us smile. Level and Checks gives you detailed settings for the security on your computer. If you're not familiar with the advanced options, read the descriptions of the Security Level choices to pick one. In Permissions, you can set the file permissions and owners for different directories. The Firewall module edits options for your Internet firewall.

### System

Options are here for many of the more frequent tasks you might have to do. Menus enables you to edit the main menu. The Display Manager is actually for choosing the login manager. In Services, you can set which background processes run on boot and start or stop each service. Fonts is for installing new fonts and seeing what you have. The Date & Time module adjusts the date, time, and time zone. You can also choose to sync to a network time server. Logs is the place to read the system logs for your computer (lists of events and errors that are confusing to read but can help in troubleshooting). Console brings up a root terminal to use. The Users and Groups module (see Figure 3.4) shows options for adding, editing, and deleting users and groups. In the Backups module, you see choices to set up regular backups of your data.

### Software Management

These modules provide a convenient way to add, remove, and browse the packages on your system. You need your install disks for the Install module. The Updates module opens the Mandrake Update tool that you will use later.

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_108_0.png)

Figure 3.4
The Users Management tool in the MandrakeLinux Control Center.

## TOOL KIT, 3.2: How to Do "Important" Stuff in Mandrake

So, you know what you can find in the MandrakeLinux Control Center, but sometimes you want to cut through the levels of menus and icons to get right to what you are trying to do. When you have something boring to do that can be called maintenance or a utility, you usually don't feel like wasting time figuring out how to get it done. Here are a few common utility tasks you might need to know how to do.

### Change Your Password (Two Methods)

- 1. Main menu > System > Configuration > Configure Your Desktop
   (from inside the KDE Control Center) System > User Account
- 2. Main menu > System > Configuration > Configure Your Computer
   (from inside the MandrakeLinux Control Center) System > Users and Groups

### Change the Root Password

Main menu > System > Configuration > Configure Your Computer  
(from inside the MandrakeLinux Control Center) System > Users and Groups  
(on the menu) Options > Filter System Users (edit the root user)

### Manage Users and Groups

Main menu > System > Configuration > Configure Your Computer  
(from inside the MandrakeLinux Control Center) System > Users and Groups

### Change the Date and Time

Main menu > System > Configuration > Configure Your Computer  
(from inside the MandrakeLinux Control Center) System > Date and Time

### Mount Disk Partitions and File Systems

Main menu > System > Configuration > Configure Your Computer  
(from inside the MandrakeLinux Control Center) Mount Points

### Start or Stop a Service

Main menu > System > Configuration > Configure Your Computer  
(from inside the MandrakeLinux Control Center) System > Services

### Read the Logs

Main menu > System > Configuration > Configure Your Computer  
(from inside the MandrakeLinux Control Center) System > Logs

## Printing

Some people print everything. They look up a Web page. They print it. They receive an e-mail. They print it. They open any file at all. They print it. Have you met these people? Okay, I should probably be quiet because you might be a very printy person. I'm not against those of the printy sort. I guess I just don't understand the constant printing. I am glad to let my printer feel lonely. The fewer small pieces of paper I have lying around me, the happier I am. Still, sometimes everyone needs to print something.

Luckily, setting up printers in Linux is easy. Now, I know that the moment I said that, eight people just had a problem setting up a printer in Linux. It's easy compared to connecting other hardware. It's easy like using canned cheese spread. It's easy like a Sunday morning. Well, maybe most hardware in Linux, it's easy for certain brands and models. Support is best for HP and Epson printers, especially inkjet printers. To find out if your printer is supported, you can check the manufacturer's documentation and Web site. Some companies acknowledge Linux and let you know. Otherwise, there is also a great site online for Linux printing, http://www.linuxprinting.org, where you can check whether your printer is supported, see which drivers work best, and look at suggested printers before you buy.

Setting up your printer can involve different steps, contingent on the printer being directly connected to your computer or if you are connecting to the printer over a local area network.

### Print Management in Fedora with GNOME

Before you spend a lot of wasted time trying to set up a printer that will not work with Linux, check the Linux Printer Compatibility Database online at http://www.linuxprinting.org/printer_list.cgi. While you are on the Linux Printing site, you can grab drivers for your printer, but most compatible printer drivers are already included in Fedora.

### Adding and Configuring a Printer

Print Manager is one of the default icons on your bottom panel in Fedora, so click on it if it is still there. You can also open the Print Manager by going to the
