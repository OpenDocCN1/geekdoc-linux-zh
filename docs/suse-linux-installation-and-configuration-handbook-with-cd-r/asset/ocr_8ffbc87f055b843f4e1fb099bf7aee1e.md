# Kernel requirements:

+   - Network Device Support
+   - PPP (point-to-point) support
+   - SLIP (serial line) support

# Configuration Basics

Before you start setting up the system for dial-in, you must configure and set up your hardware. To set up the modem or ISDN equipment, see Chapter 23, “Connectivity to the Internet.” After you have set up your modem and made sure that it can dial out, you can start configuring your SuSE Linux for dial-in.

The following are the three steps for configuring SuSE Linux for dial-in:

+   1. Set up mgetty.
+   2. Set up the authentication method.
+   3. Set up pppd.

In practice, these are the only steps required to configure either a simple dial-in server or a full ISP dial-in server. One difference does exist, however—the privileges and security issues you must be aware of if you are configuring a full ISP.

# getty and mgetty+sendfax

getty is a special program invoked by init to enable users to log in. It opens a tty line and sets its mode. An example of a tty line is your console. It then prints the login prompt, reads the username, and starts a login process for the user.

On the other hand, mgetty is a getty replacement with hayes-compatible data and data/fax modems. Using these capabilities, mgetty enables system logins over ttys, therefore enabling users to log in over serial connections. mgetty can be set up to receive fax as well as voice. In this chapter, we will cover only the capabilities that cause your computer to act as a dial-in server.

# mgetty Configuration Files

Older versions of mgetty required that you configure it through the source code definitions. Luckily, this has changed and all the configurations for mgetty can be done through the configuration files located in /etc/mgetty+sendfax. The directory contains various configuration files:

+   - dialin.config—If you have installed a caller ID service, you can tell mgetty to (or not to) answer certain phone numbers by configuring the entries in this file.