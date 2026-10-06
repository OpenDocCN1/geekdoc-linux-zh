# Running the Installer

The Debian installation process consists of two stages. The first stage is used to establish the Debian installation on your hard drive. The second stage boots the newly installed Debian system and performs additional installation and configuration tasks.

Before you begin installing Debian to your hard disk, be sure to back up any data that is important to you. A simple mistake partitioning can result in losing some or all of your data. Refer to Chapter 7 for information on disk partitioning. It can help you decide how to use your hard disk or ever resize disk partitions to make room for the new Debian installation.

# Stage 1

The first stage boots from the installation medium (generally a CD); configures hardware drivers, disk partitions, and file systems; and copies a set of essential packages known as the base system. Here's the procedure:

+   - Boot the CD that comes with this book and type linux from the boot prompt to begin the Debian installer.

+   - After the installation has finished, you are presented with the series of menus that make up the installation process. Use the arrow keys to navigate through the menus and select your language, region, and keyboard mapping.

+   - The next step is to configure the network connection. This step is skipped automatically if no network card is detected in your system.

If a network card is detected in your system, the installer will attempt to automatically detect the network using the DHCP protocol. This involves the computer sending requests on the network for configuration details from a DHCP server. Most networks and broadband routers support this service.

If the DHCP configuration fails, you will be presented with four options:

+   - retry — Select this option if you suspect that there was a temporary problem that prevented your computer from communicating with the DHCP server.

+   - retry with hostname — Select this option if your network provider requires you to enter a DHCP hostname. This used to be common on cable modem networks, but is rarely seen anymore.

+   - manual configuration — Select this option if you have static IP address information that must be entered for your Internet connection.

See Chapter 7 for information about IP addresses, network masks, and other material related to setting up a network connection.