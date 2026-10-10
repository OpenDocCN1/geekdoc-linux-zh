
most cases.

Finally, **Xconfigurator** prompts you to select the video modes you wish to use; select one or more modes by pressing [Space]. **Xconfigurator** then writes a configuration file containing all of your choices to /etc/X11/XF86Config.

## 2.4.15 Configuring Networking

After assisting you in configuring an X server, the installation program gives you an opportunity to configure (or reconfigure) networking. If you are installing from CD-ROM or from a local hard disk, the installation program asks if you want to configure networking. If you choose **No**, your Red Hat Linux system will be a standalone workstation. If you choose **Yes**, you may configure networking as described below.

If you are installing Red Hat Linux via NFS or FTP, you will have already configured temporary networking information. The install program offers you three choices:

- Keep the setup you have been using to install with; all the networking information you entered previously becomes part of your system’s permanent configuration.
- Reconfigure networking; the installation program presents the network configuration dialogs described below with the values you used during installation filled in as defaults. Choose this if your system will be installed on a network other than the one you used to install Red Hat Linux.
- Don’t set up networking at all; your system will not have networking configured. Choose this if you installed your system over a network, but it will be used as a standalone workstation.

### Network Configuration Dialogs

After the installation program has found your network card, it presents several dialogs for configuring your system’s permanent TCP/IP networking. This feature allows greater flexibility if you want to install from a network other than the one where the machine will “live”. Figure 2.5 contains example networking information.

The first dialog asks you for IP and other network addresses (see Figure 2.6). Enter the **IP address** you are using during installation and press `Enter`. The installation program attempts to guess your **Netmask** based on your IP address; you may change the netmask if it is incorrect. Press `Enter`. The installation program guesses the **Default gateway** and **Primary nameserver** addresses from your IP address and netmask; they may change them if they are incorrect. Choose **OK** to continue.

The second dialog prompts you for a domain name, a hostname, and other networking information (see Figure 2.7). Enter the **Domain name** for your system and press `Enter`; the installation program carries the domain name down to the **Host name** field. Enter the hostname you are using in front of the domain name to form a fully qualified domain name (FQDN). If your network has more than one nameserver, you may enter IP addresses for additional nameservers in the **Secondary nameserver** and **Tertiary nameserver** fields. Choose **OK** to continue.

## 2.4.16 Configuring a Printer

After you have set up networking, the installation program asks whether you would like to configure a printer. If you choose **Yes**, a series of dialogs will assist you in configuring your printer. The following information applies to all printers:

- **Printer Connection:** Where the printer is connected—*local*, *remote*, or *LAN-Manager*.
    - **Local printer:** A local printer is connected directly to the system you’re installing on.
    - **Remote printer:** A remote lpd printer is connected to another machine on the network which runs lpd (the print server used on Linux and many other flavors of Unix).
    - **LAN-Manager printer:** A LAN-Manager printer is connected to another machine on a LAN-Manager-style (SMB) network.
- **Queue:** The name of the printer queue you are creating.
- **Spool Dir:** The directory where print jobs are stored while they are being printed.
- **Type of Printer:** The make and model of your printer; if your printer doesn't appear on the list, you may have luck by choosing a printer make and model which is similar to yours.
- **Paper Size:** The size of paper your printer uses.
- **Resolution:** The resolution, in dots per inch, you wish your printer to use.
- **Color:** If you have a color printer, the color depth you wish your printer to use.

**Local** printers also require the following information:

- **Printer Device:** The printer's port your printer is attached to.

**Remote LPD** printers also require the following information:

- **Remote Host:** The name or IP number of the host the remote printer is connected to.
- **Remote Queue:** The name of the remote printer queue.

**LAN Manager** printers also require the following information:

- **LAN Manager Host:** The name of the host the SMB printer is connected to.
- **LAN Manager IP:** The IP number of the host the SMB printer is connected to; this is optional.
- **Share Name:** The name of the shared SMB printer.
- **Username:** The username you need to use to access the SMB printer (typically `guest` for Windows servers, or `nobody` for `samba` servers).
- **Password:** The password you need to use to access the SMB printer (typically blank).

When you have finished configuring a printer, the installation program will ask you to confirm the choices you made. After you confirm them, you may configure another printer, or you may continue with the installation.

## 2.4.17 Configuring the Clock

Next, the installation program presents a dialog to help you configure your Red Hat Linux system's timezone.

If you wish to set the hardware (CMOS) clock to GMT (Greenwich Mean Time, also known as UTC, or Coordinated Universal Time), select **Hardware clock set to GMT**. Setting your hardware clock to GMT means your Red Hat Linux system will properly handle daylight savings time, if your timezone uses it. Most networks use GMT.

Select the timezone your system will be operating in from the list, and press `Enter`.

If you wish to change your timezone configuration after you have booted your Red Hat Linux system, you may use the `/usr/sbin/timeconfig` command.

## 2.4.18 Setting a Root Password

After you have set up your system's timezone, the installation program prompts you to set a *root password* for your system; this is the password you will use to log into your Red Hat Linux system for the first time.

The root password must be at least six characters long; the password you type is not echoed to the screen. You must enter the password twice; if the two passwords do not match, the installation program will ask you to enter them again.

You ought to make the root password something you can remember, but not something that is easy for someone else to guess. Your name, your phone number, `qwerty`, `password`, `root`, `123456`, and `anteater` are all examples of poor passwords. Good passwords mix numerals with upper and lower case letters and do not contain dictionary words: `Aard387vark` or `420BtttTNT`, for example. Remember that the password is case-sensitive. Write down this password and keep it in a secure place.

**Please Note:** The *root* user (also known as the *superuser*) has complete access to the entire system; for this reason, logging in as the root user is best done only to perform system maintenance or administration, so that critical system files are not inadvertently changed, moved, or deleted. Please see Section 8.1 for instructions on how to add a user for yourself after you reboot your system.

## 2.4.19 Installing LILO

In order to be able to boot your Red Hat Linux system, you usually need to install **LILO** (the Linux LOader). You may install **LILO** in one of several places:

**The Master Boot Record (MBR)** is the recommended place to install **LILO**, unless another operating system loader (e.g., System Commander or OS/2’s Boot Manager) is already installed there. When your machine boots, LILO starts and presents the `boot:` prompt; you can boot Red Hat Linux or any other operating system you configure LILO to boot (see below).

**The first sector of your root partition** is recommended if you are already using another boot loader on your system (such as OS/2’s Boot Manager); then you can setup that boot loader to start **LILO** and boot Red Hat Linux.

**The first sector of a floppy diskette** is an alternative either of the above options; to boot Red Hat Linux, insert the **LILO** diskette into your machine’s floppy drive and reboot. LILO starts from the floppy and presents the `boot:` prompt.

Select the location you wish to install **LILO** and press **OK**. If you do not wish to install LILO, press **Skip**.

### Limitations of LILO

**LILO** is subject to some limitations imposed by most PC BIOSes. Specifically, most BIOSes can’t access more than two hard drives and they can’t access beyond cylinder 1023 (the 1024th cylinder) of any drive. Some more recent BIOSes do not have these limitations.

All the things which **LILO** needs to access at boot time (including the kernel) are located in the `/boot` directory of your root partition.
