
## Popup Windows

- All windows beyond the main display are secondary or pop-up windows, and provide additional and amplifying information about selected networks, groups, or clients, as well as statistics and additional interesting information.
- The information provided on the wireless card power and network location pop-up windows is wholly dependent upon the wireless card drivers and/or firmware. Kismet does not calculate signal or noise information, rather it simply reports it.

## Customizing the Panels Interface

- Both the network list and client list can be modified to the user's specifications by editing the `kismet_ui.conf` file.
- Kismet's color scheme, including the background, borders, and default color-coding of networks, can be modified as well.

## Third-Party Front-ends

- Third-party front-ends are GUIs designed to supplement or replace the Kismet client panels interface.
- Third-party clients are available to run on both Linux and Windows.

## Configuring the Kismet Server

### Solutions in this chapter:

- The Kismet Config File
- Kismet.conf
- Summary

## Introduction

The Kismet server is controlled primarily from one big scary configuration file. Usually located in `/usr/local/etc`, the `kismet.conf` file is where you’ll spend most of your configuration time. Anyone who’s spent any time working on config files will find themselves pretty comfortable. It is an untapped resource for both the Kismet beginner and even for experts who have been using Kismet for a while. Not many people go through and check out the extent of the configuration options available to them. There’s a great amount of information that can be tracked and recorded by Kismet, as well as filtering and targeting of certain information. Understanding what options are available will help you use Kismet in the best possible way for your needs.

## The Kismet Config File

The config file is not as scary as it may seem. It is very large, however, because Dragorn was kind enough to leave a lot of very verbose comments about the various options. Some areas are fairly self-explanatory while others are not. This section will go through, almost line-by-line and examine and explain each of them. The comments are good, however some areas are open to tweaks not specified in the comments, and a lot of power can be revealed once you start digging into the config file.

## Kismet Parameters

The `kismet.conf` config file can be edited directly with your favorite UNIX text editor (such as vi, pico, emacs), just be aware of word wrapping and UNIX file format. The config file is parsed at runtime by the server and expects a UNIX text file. DOS and UNIX use different control characters for their text files and as such, using a DOS or windows editor on a UNIX text file will probably change it and make the file unreadable to the server. In general, if you are editing the `kismet.conf` file, use a UNIX editor. This can be either a native Linux application, or an editor through Cygwin if you are running under windows or some other UNIX text format-capable editor.

Comments in the `kismet.conf` file are lines starting with a “#” symbol. These are often comments or example configurations and can usually guide you to what options you need to set. Lines that do not start with a comment are the actual parameter variables acted upon by the server. It’s a good idea to comment out the existing line by putting a “#” in front of the line and adding a new line with the adjusted parameter. This way if something goes wrong, you know what the original parameter was.

### Kismet.conf

```
# Kismet config file
# Most of the "static" configs have been moved to here -- the command line
# config was getting way too crowded and cryptic. We want functionality,
# not continually reading --help!
```

The Kismet server used to be controlled through command-line parameters (many of which still can be used), but as the program and functionality grew, it became a huge effort to set all the command-line arguments for sources, ports, and so forth. So everything was moved into the `kismet.conf` file. The above lines are the beginning of the `kismet.conf` file, and is a throwback to those early days when people spent forever looking at the `--help` command line switches.

```
# Version of Kismet config
version=2007.09.R1
```

This line indicates the version of the config file itself, not the version of the server or any other portion of the program. A lot of people confuse this line with the server version and wonder why their server is three versions back. The config file doesn't change as often as the rest of the tool suite, so it has a separate version number listed on this line.

```
# Name of server (Purely for organizational purposes)
servername=Kismet
```

This parameter is one of those often-overlooked sections of the config, and it's right at the top. The `servername` parameter allows you to name the server for your own organizational purposes. This is particularly useful if you are monitoring several remote servers with one client instance. You could have servers named after location (`server_north_east`, `server_north_west_warehouse`) or channel (`server_ch1`, `server_ch2`) or however you want to keep things sane. The server name must not contain any spaces, so use underscores or dashes in place of spaces. This allows you to know which server you're connected to and its location for either troubleshooting purposes or for incident tracking. It has no real affect on performance; it's just useful for keeping you sane, particularly in large installations.

```
# User to setid to (should be your normal user)
uiduser=your_user_here
```

This line is often misunderstood by people just beginning with Kismet. This is the user that Kismet will run it’s processes as once it’s started. Kismet requires root access to set monitor mode and other options, then it drops privileges on the Kismet processes to the user specified in this parameter.

```
sqliduser=foo
```

The above is an example, where “foo” is a normal user account on the system.

**NOTE**

As noted in the chapter on basic Kismet install, unless you build Kismet Set User ID (SUID) root, you need to have a normal non-privileged user on the system. This is for security reasons. The user specified here also has to have write permission on the directory where you are storing your captured data and logs. A major problem people trip on is that they run Kismet as root and specify root as the SETUID user. Unless you built it SETUID root, this will halt Kismet from starting. They also make the mistake of logging in as root, running Kismet from /root and the server fails to start as the SETUID user does not have write permission on the /root directory. The simple solution is to login as a normal user and either su to root or use sudo to start Kismet.

Specify the username of a non-privileged (non-root) user on the system and make sure that wherever you store the data it has write permission. The logical place for this is the non-privileged users home directory. The best order to run Kismet to avoid problems is to login as a normal user, change to the directory you want the resulting data saved to, then “su” to root and then run Kismet.

```
# Do we try to put networkmanager to sleep? If you use NM, this is probably # what you want to do, so that it will leave the interfaces alone while # Kismet is using them. This requires DBus support! networkmanagersleep=true
```

This line in the config file tells Kismet to use Dbus to disable Network Manager, the common gnome desktop manager applet, to disable itself for the duration of the Kismet session. After Kismet exits, the network manager will resume control.

**NOTE**

> Many modern Linux distributions use fancy X widgets to control the network cards. It’s an attempt at making the system user friendly and avoiding users to have to go to the command line to connect to a wireless network. The problem is, if we want to do anything weird with the card, such as monitor mode, these network monitor programs fight for control of the card and can cause no end of grief for Kismet.
>
> If you have any weird scanning situations such as things randomly stopping scanning or getting stuck on one channel and not hopping, this is a likely candidate. For the most part, you’ll want this option enabled.
>
> In some situations, this may cause issues. The most common will be when you are scanning with one interface but using the network manager to control another for communication (such as an intrusion detection system (IDS) setup reporting to a server). Kismet disables network manager for all interfaces, wired and wireless. If you run into problems with the network manager being disabled, you may want to not use the network manager at all and manually configure the other interfaces.

```
# Sources are defined as:
# source=sourcetype,interface,name[,initialchannel]
# Source types and required drivers are listed in the README under the
# CAPTURE SOURCES section.
# The initial channel is optional, if hopping is not enabled it can be used
# to set the channel the interface listens on.
# YOU MUST CHANGE THIS TO BE THE SOURCE YOU WANT TO USE
```

Probably one of the most important areas of the config file; where do we get our data. The source line tells Kismet what it needs to know to get data into the program so we can start scanning. Each source has three parameters: a Kismet source name for the specific type of card, the interface name, and a logical name found in the Kismet client. The Kismet README has a list of compatible sources and their proper interface names.

| Driver | Description | Link / Interface |
| :--- | :--- | :--- |
| hostap | Prism/2 Linux HostAP 0.4 | http://hostap.epitest.fi/ |
| | Capture interface | `wlanX` |
| | HostAP drivers drive the Prism/2 chipset in access point | |
