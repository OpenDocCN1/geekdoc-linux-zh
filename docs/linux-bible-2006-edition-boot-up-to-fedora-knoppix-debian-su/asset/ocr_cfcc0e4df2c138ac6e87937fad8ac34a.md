# Chapter 9 ♦ Running Debian GNU/Linux 311

send messages, but this configuration still enables you to send and receive mail using programs such as Mozilla Mail and News, Mozilla Thunderbird, Evolution, and Sylphed that include built-in support for sending messages using the SMTP protocol. This is also the option you want will be setting up this system to act as a mail server based on the instructions in Chapter 25.

Enter the mail name for this system (the default is what you want), and choose the user to whom you want system messages to go. In most cases, you want to select the user account that was added earlier.

You now have a fully functional Debian GNU/Linux. The server does not have any extra packages installed but is ready to be used for the LAMP and mail server examples in this book (which you can find in Chapters 24 and 25, respectively). There’s no graphical interface installed yet, which means all interaction will be through the command line. Take some time, as needed, to browse through Chapter 2 and familiarize yourself with the command line before continuing with the next section.

You can find a complete desktop in the desktop task. See the "Installing Package Sets (Tasks) with Tasksel" later in the chapter for more information.

# Managing Your Debian System

Some of the basic tasks that you may encounter while running Debian GNU/Linux include package installation, configuration, and removal, as well as handling some situations that you may come across.

All these steps require that you be logged in as the superuser (root). If you have finished installing the system, you can log in from root from the login prompt.

# Configuring Network Connections

Debian includes a set of tools for managing most types of network interfaces, including Ethernet, PPP, wireless, and even ATM. You may find that you need to add or change network settings after the system has been installed.

# IP Networks: Ethernet and Wireless

On Debian systems, standard network connections are configured in the /etc/network/interfaces file. If you have a network card configured to obtain an IP address automatically, this file will look like this:

```
# This file describes the network interfaces available on
# your system and how to activate them. For more information,
```