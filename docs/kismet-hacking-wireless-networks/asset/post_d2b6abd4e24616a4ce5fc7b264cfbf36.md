
# Default text
textcolor=white
# Window borders
bordercolor=green
# Titles
titlecolor=hi-white
# GPS and APM info
monitorcolor=hi-white
# WEP network color
wepcolor=hi-green
# Factory network color
factorycolor=hi-red
# Open color
opencolor=hi-yellow
# Decloaked network color
cloakcolor=hi-blue

If the default black, green, and yellow color scheme for the client is not to your liking, you can change any of the elements' colors you want. Just change any of the elements' config lines to black, red, yellow, green, blue, magenta, cyan, or add “hi-” in front of the color name to make it bold.

### Command-Line Switches

Just as the server, you can specify command-line switches for the Kismet client. This does require you to start the Kismet server separately using *kismet_server*. You can’t use the Kismet script that launches both the server and client together. The command-line switches override any settings in the *kismet_ui.conf* file.

- **-f, --config-file <file>**: Use alternate config file
  Some of the options for the client come from the server config file, so if you specify an alternate server config file, the client needs to know about it.

- **-u, --ui-config-file <file>**: Use alternate UI config file
  Some users like to have one config file with the columns a certain way, and another with different columns listed. Using the *-u* switch, you can easily change from one to another.

- **-q, --quiet**: Don’t play sounds
  Sometimes sound is useful, other times it's not. This option will disable it for you for this run of the client.

- **-s, --server <host:port>**: Connect to Kismet host and port
  Probably the most common use of command-line switches for the client, is specifying an alternate server. If you're running multiple servers, maybe in an IDS setup, you can specify the IP and port at runtime with the -s switch.

- **-g, --gui <type>**: GUI type to create (curses, panel)
  If you need to switch between a panel and curses interface for a session (there shouldn't be many) you can specify it here. There are only two choices: panel and curses.

- **-C, --columns <list>**: Columns to display initially (comma separated)
  Instead of multiple config files, you can manually specify what columns you want, in the order you want from the command line. Valid options are the same as in the config file, listed earlier in the chapter or in the Kismet README file.

- **-r, --reconnect**: Try to reconnect after the client/server connection fails.
  If you are on a flakey or a high latency connection to a remote server, the client might disconnect occasionally. The -r switch will automatically have the client try and reconnect the client to the server if it is disconnected.

- **-c, --client-columns <list>**: Columns to display for client info
  As with the network columns, you can specify as comma-separated names, which columns and the order you want them for client devices that are detected. Valid options are the same as in the config file, listed earlier in the chapter or in the Kismet README.

- **-v, --version**: Kismet version
  The -v option will print the version number of the client to the command line.

- **-h, --help**: What do you think you're reading?
  Finally, the -h option will pull up the list of command-line switches in case you don't have this book handy.

### Summary

The Kismet client has a great deal of configuration available to it. Proper configuration can give you the information you want, where and when you need it. Adjusting the columns puts the information at your fingertips and can make your life easier and hopefully more productive.

# Chapter 7

# Server.conf File Advanced Configuration

Solutions in this chapter:

- Asus EEEPC installation
- Kismet On Windows
- Wardriving in a Box
- Monitor Installation
- Summary

# Introduction

Kismet is capable of some amazing feats. It’s highly useful in a mobile, rogue-hunting role as it is in a stationary IDS setup. This chapter will show you the various ways that Kismet can be used. Kismet is used all over, from mobile rogue-hunting systems, to site surveys, to full IDS setups for monitoring the airwaves around your wireless installations.

## Asus eeePC Installation

In 2007, Asus released the eeePC, a diminutive sub-notebook running Linux. These laptops use a solid state drive, which means fast boot times and they can put up with a lot of movement. The eeePC comes with xandros Linux installed and with an atheros wireless chipset, making it a nice light and portable Kismet rig.

The eeePC’s are all fairly identical except for disk space and random access memory (RAM), but the chipsets are consistent. Installation on the default Linux install is fairly easy. A few downloads and packages and you’re good to go. You may choose to put another Linux distro or even Windows onto an eeePC, however, those instructions are in other chapters. In this case, we are going to use the eeePC as a quick and light mobile search and sniff rig for your office.

## Installation and Updating

Once you’ve opened your eeePC, the first thing you want to do is update it. This is isn’t necessary for the Kismet installation, but is a good idea since the eeePC originally shipped with a vulnerable version of samba, which could lead to bad things.

To update you can use the update features of the add/remove software under the settings menu on the eeePC, but we’ll be using the command line since it’s more thorough.

First connect your eeePC to the Internet and open a command shell with:

```
ctrl-alt-t
```

You’ll need to change to the super user, which is easiest with:

```
sudo su
```

Be careful from now on, you are now super user and if you aren’t careful, you can cause major damage to your operating system installation.

Now we need to update the *apt* cache:

```
apt-get update
```

This tells the system to see what packages are available from asus, and if any are newer than what are installed. Upgrade your system to the latest versions available with:

```
apt-get upgrade
```

Apt will probably give you a large list of packages to install and ask for confirmation. This can take a few minutes.

## Install Development Tools

By default, the eeePC does not ship with a compiler and most of the basic development tools, however, we can add them, but not from the asus source.

The eeePC is based on Xandros Linux, which is debian-based. This basically means that we can use debian packages fairly safely with the default operating system (OS). This is fairly easy and just requires us to add the debian stable packages to our repository list and load away.

To start, if you haven't already got one open, open a terminal window with:

```
ctl-alt-t
```

Also, make sure you are root with:

```
sudo su
```

Now, you'll need to select a mirror site to download your packages from. Go to http://www.debian.org/mirror/mirrors_full and select a mirror from the list. For the examples, we'll be using the generic ftp.debian.org. You'll need to add the mirror and path you choose to the /etc/apt/sources.list.

```
deb http://ftp.debian.org/debian/ stable main contrib non-free
```

Once again, we need to update our sources to include the new repository:

```
apt-get update
```

Once apt knows about the new packages available, we can install the build tools we need to build Kismet:

```
apt-get install build-essential
```

If all goes well, apt will load the necessary build tools. We can now load the dependencies we need to install to build Kismet. The required ones are:

- libcurses5-dev
- libcap0.8-dev
- zlib1g-dev

This is necessary to get Kismet running. If you want to include gpsmap, you'll need to include the following:

- imagemagick
- libexpat1-dev
- libgmp3-dev

You can add all of these in one `apt-get` install command, just list them all on one line with spaces between packages.

```
apt-get install libcurses5-dev libcap0.8-dev zlib1g-dev imagemagick libexpat1-dev libgmp3-dev
```

This should take a few minutes.

Once everything is installed, you can download the latest Kismet stable package from http://www.kismetwireless.net. Check the downloads section for the latest release version. If you want to track any changes to the source since the last release, you'll need to install subversion to get the bleeding-edge development source. Fortunately, this is easy since we have `apt` set up:

```
apt-get install subversion
```

followed by:

```
svn co https://svn.kismetwireless.net/code/trunk kismet-devel
```

This will download the latest source into the `kismet-devel` directory you are working in, so make sure it’s where you want it. If you want to update this source in the future, go to the directory and type `svn update` and any new source changes will be merged into the existing source. Once you have the source, if you need to unpack it, do so now. Switch to the Kismet source directory and just like any other install, run:

```
./configure
make
make install
```

Check the output from configure and make sure all dependencies that you want/need are satisfied, and hopefully all will work fine when you run `make`. Once Kismet is built and installed, you still need to configure the server. This part is easy once you know what needs to happen. The `Kismet.conf` file needs the following lines changed:

```
suiduser=user
source=madwifi_g,wifi0,<descriptive name here>
```
