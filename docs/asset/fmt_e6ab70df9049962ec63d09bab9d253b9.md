
# LAB 69

## Install and Configure X11

**Lab Objective:**

Learn about the X11 window system and how to configure it.

**Lab Purpose:**

In this lab, you will explore various aspects of X11 configuration.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice), and a running X11 system. If you aren't sure whether your system runs X11, test with `sudo ps -ef | egrep -i x11\xorg`

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

***Task 1:***

Open the Terminal and attempt to look at `/etc/X11/xorg.conf` or `/etc/X11/xorg.conf.d.` These paths may not exist—on a default Ubuntu 18.04 VM install, they don't. If not, run `blah` and take a look there instead—for example, in `/usr/share/X11/xorg.conf.d`. You are just trying to view some example Xorg config files.

A typical X11 config will have one or more sections, each section dealing with a single device; for example, a monitor, or a graphics card, or an input device. Within a section, a given device may have several directives, like specifying a driver or various options for the device.

If you are setting up Xorg on a new server, you can run `Xorg -configure` to generate a new configuration. This is not recommended on a machine of any importance, as it is easy to mess up. (Though a backup should be automatically created.)
