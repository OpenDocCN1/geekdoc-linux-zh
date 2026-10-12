
![](img/3d09de050edc8aef2a604e36a4127b47_42_0.png)

Figure 2.13: Selecting Packages

## Package Installation

After all package dependencies are resolved, the installation program begins to install packages; it leaves a complete log of what it installs in `/tmp/install.log` on your Red Hat Linux system.

## 2.4.12 Selecting a Keymap

After it has finished installing all the packages you selected, the installation program presents a list of available keymaps to install (see Figure 2.15). Select the keymap you wish to use on your Red Hat Linux system and press `Enter`; the installation program installs that keymap immediately.

If you wish to change your keymap after you have booted your Red Hat Linux system, you may use the `/usr/sbin/kbdconfig` command.

## 2.4.13 Configuring a Mouse

To configure your mouse, choose the mouse type that best matches your mouse and press `Enter`. If you have a 2 button mouse and want to emulate the third (middle) button by clicking the left and right buttons at the same time, choose **Emulate 3 Buttons**.

If you choose a serial mouse, the next dialog prompts you for the serial (COM) port your mouse is connected to. Choose the correct port and press `Enter`.

> **Please Note:** If your mouse is connected to a *PS/2 mouse port*, you should select **PS/2 Mouse**, no matter what kind of mouse it is.

If you wish to change your mouse configuration after you have booted your Red Hat Linux system, you may use the `/usr/sbin/mouseconfig` command.

## 2.4.14 Configuring X Windows

After setting up your mouse, if you installed the X Windows packages, you have the opportunity to configure your X server. If you did not *choose* to install the X Window System, you may skip to Section 2.4.15 below.

![](img/3d09de050edc8aef2a604e36a4127b47_43_0.png)

### Configuring the Metro-X Server

If you are installing from an Official Red Hat Linux/Intel CD, you may install one copy of MetroLink’s Metro-X server, a high-quality commercial X server for Linux. Please see the MetroLink license (paper copy) accompanying your Red Hat Linux CD for license information. If you choose to use Metro-X, the install Program launches the Metro-X configuration utility `configX`; please see Chapter 5, Section 5.3 for more information on how to use `configX`.

### Configuring an XFree86 Server

If you wish to use XFree86 (because Metro-X may not support your video card, because you have already installed Metro-X on another machine, because Metro-X was not included with your copy of Red Hat Linux/Intel, or because you simply prefer to use XFree86), the install program launches the `Xconfigurator` utility, which is described in detail in Chapter 5, Section 5.2.

`Xconfigurator` first presents a list of video cards. Select your video card from the list and press `Enter`. If your video card does not appear on the list, XFree86 may not support it; however, if you have technical knowledge about your card, you may choose **Unlisted Card** and attempt to configure it anyway.

Once you have selected your video card, the installation program installs the appropriate XFree86 server, and *Xconfigurator* presents a list of monitors. If your monitor appears on the list, select it and press `Enter`. Otherwise, select *Custom*. If you do select *Custom*, *Xconfigurator* prompts you to select the horizontal sync range and vertical sync range of your monitor (these values are generally available in the documentation which accompanies your monitor, or from your monitor’s vendor or manufacturer).

> **Please Note:** It is not recommended to select a monitor “similar” to your monitor unless you are certain that the monitor you are selecting does not exceed the capabilities of your monitor. If you do so, it is possible you may overclock your monitor and damage or destroy it.

Next, *Xconfigurator* prompts you for the amount of video memory installed on your video card. If you are not sure, please consult the documentation accompanying your video card. It ought not to damage your video card by choosing more memory than is available, but the XFree86 server may not start correctly if you do.

If the video card you selected might have a video clockchip, *Xconfigurator* presents a list of clockchips. The recommended choice is *No Clockchip Setting*, since XFree86 can automatically detect the proper clockchip in most cases.

Finally, *Xconfigurator* prompts you to select the video modes you wish to use; select one or more modes by pressing `Space`. *Xconfigurator* then writes a configuration file containing all of your choices to `/etc/X11/XF86Config`.

![](img/3d09de050edc8aef2a604e36a4127b47_44_0.png)

## 2.4.15 Configuring Networking

After assisting you in configuring an X server, the installation program gives you an opportunity to configure (or reconfigure) networking. If you are installing from CD-ROM or from a local hard disk, the installation program asks if you want to configure networking. If you choose **No**, your Red Hat Linux system will be a standalone workstation. If you choose **Yes**, you may configure networking as described below.

If you are installing Red Hat Linux via NFS or FTP, you will have already configured temporary networking information. The install program offers you three choices:

- Keep the setup you have been using to install with; all the networking information you entered previously becomes part of your system's permanent configuration.
- Reconfigure networking; the installation program presents the network configuration dialogs described below with the values you used during installation filled in as defaults. Choose this if your system will be installed on a network other than the one you used to install Red Hat Linux.
- Don't set up networking at all; your system will not have networking configured. Choose this if you installed your system over a network, but it will be used as a standalone workstation.

![](img/3d09de050edc8aef2a604e36a4127b47_45_0.png)

### Network Configuration Dialogs

After the installation program has found your network card, it presents several dialogs for configuring TCP/IP networking. This information is only used during the installation process; you will be able to configure permanent networking information later. This feature allows greater flexibility if you want to install from a network other than the one where the machine will "live". Figure 2.4 contains example networking information.

The first dialog asks you for IP and other network addresses (see Figure 2.5). Enter the **IP address** you are using during installation and press `Enter`. The installation program attempts to guess your **Netmask** based on your **IP address**; you may change the netmask if it is incorrect. Press `Enter`. The installation program guesses the **Default gateway** and **Primary nameserver** addresses from your IP address and netmask; you may change them if they are incorrect. Choose **OK** to continue.

The second dialog prompts you for a domain name, a hostname, and other networking information (see Figure 2.6). Enter the **Domain name** for your system and press `Enter`; the installation program carries the domain name down to the **Host name** field. Enter the hostname you are using in front of the domain name to form a fully qualified domain name (FQDN). If your network has more than one nameserver, you may enter IP addresses for additional nameservers in the **Secondary nameserver** and **Tertiary nameserver** fields. Choose **OK** to continue.

![](img/3d09de050edc8aef2a604e36a4127b47_46_0.png)

## 2.4.16 Configuring the Clock

After you have set up networking, the installation program presents a dialog to help you configure your Red Hat Linux system’s timezone.

If you wish to set the hardware (CMOS) clock to GMT (Greenwich Mean Time, also known as UTC, or Coordinated Universal Time), select **Hardware clock set to GMT**. Setting your hardware clock to GMT means your Red Hat Linux system will properly handle daylight savings time, if your timezone uses it. Most networks use GMT.

Select the timezone your system will be operating in from the list, and press <u>Enter</u>.

If you wish to change your timezone configuration after you have booted your Red Hat Linux system, you may use the `/usr/sbin/timeconfig` command.

## 2.4.17 Setting a Root Password

After you have set up your system’s timezone, the installation program prompts you to set a *root password* for your system; this is the password you will use to log into your Red Hat Linux system for the first time.

The root password must be at least six characters long; the password you type is not echoed to the screen. You must enter the password twice; if the two passwords do not match, the installation program will ask you to enter them again (see Figure 2.16).

You ought to make the root password something you can remember, but not something that is easy for someone else to guess. Your name, your phone number, *qwerty*, *password*, *root*, *123456*, and *anteater* are all examples of poor passwords. Good passwords mix numerals with upper and lower case letters and do not contain dictionary words: Aard387varK or 410VBltlSW, for example. Remember that the password is case-sensitive. Write down this password and keep it in a secure place.

**Please Note:** The *root* user (also known as the *superuser*) has complete
