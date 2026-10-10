
## Network Configuration Fields

**TABLE 2.5 Network Configuration Fields**

| Field | Description |
|---|---|
| **General Network Options for This System** | |
| Host | The hostname and domain name of your system go here (in this example, kiara.lionresearch.org). |
| Domain | The name of the domain name where your system is located (in this example, lionresearch.org). |
| IPv4 Gateway | If your system will use another host to access nonlocal network resources (the Internet), put the address of that host here. If this system has direct Internet access, this field should be left blank. |
| Name server | The IP address of your DNS server, which is the server that resolves network names into IP addresses. |
| **Network Options Specific to This Network Interface** | |
| IPv4 Address | The IP address of this system. |
| Netmask | The netmask value for the network that this interface accesses. |
| Extra Options to ifconfig | Any extra options you need to pass to the network configuration should go here. |

If you are unclear about any of these concepts, you should read Chapters 21 and 22 before configuring the network.

> **CAUTION**
>
> If you aren’t sure what numbers or names should go in the Network Configuration screen, ask someone who will know. Never simply fill in random numbers or names if your system is on a network. If your system is connected to a network, simply inserting random numbers in the IPv4 Address field or a random hostname in the Host field is a sure way to get on the bad side of the network administrators as well as other network users. If you select an IP address that conflicts with an existing system on the network, bad things will happen, including possible denial of service to an important network resource if your IP address conflicts with that of a major server.

Use the Tab or Enter key to move between fields. When you are done, select OK to leave the configuration screen.

Depending on the type of network interface you set up, you may now be asked if you wish to bring the interface up right now. Select No, because you are almost done with the install and will be rebooting the system soon anyway.

Sysinstall will then ask you a series of questions about the network:

- **Will this machine be a leaf node (for example, will it not forward packets between interfaces)?**

  Unless this machine will be a gateway that other systems on the network will use to get to the Internet, or a router that will handle network traffic intended for other systems, you should select Yes.

- **Do you want to grant only normal users FTP access to this host (for example, no anonymous FTP connections)?**

  I suggest you select Yes unless you have already read the chapters on networking. You can always configure anonymous FTP access later on.

- **Do you want to configure this machine as an NFS server?**

  The NFS server allows you to share directories on your hard disk so that users on other systems can mount them and read and/or write files to them. Once again, unless you have read Chapter 32, “The Network Filesystem (NFS),” I suggest you select No for now, even if you know that you will need this service. NFS can be a security problem if it’s not set up properly. After you read Chapter 32, you can come back and set this up.

- **Do you want to configure this machine as an NFS client?**

  If you need to mount filesystems on your drive that are located on other systems, you need to set up the NFS client. Once again, see Chapter 32 for more information on configuring NFS.

- **Do you want to select a default security profile for this host (select No for medium security)?**

  Unless high security is absolutely critical in your environment, I suggest you select No. Later, you can customize the security settings by editing the system configuration files. These settings are very easy to change in the system configuration files.

After you select No for the last option, you see a message that tells you about the services that will be enabled in this profile. The “high” security profile will disable services such as X, so you can’t even start the X-Server on your local machine. Therefore, I suggest using the default “medium” security profile for now unless you will be running the server in an environment where security is critical. After you read this message, press Enter to continue.

## Customizing the Console

Next, you have the opportunity to customize the FreeBSD console settings. You can use these settings to customize the behavior of your keyboard, to choose which font will be used on the screen display, and to select which screensaver to use. If you select Yes to the question asking you whether you want to customize your console setting, you see a menu like the one shown in Figure 2.8.

Most of the options here are self-explanatory. Simply select any options you need to configure and then follow the onscreen instructions.

![](img/48eec858cce7dfb89da36a4d40b7daf3_78_0.png)

**FIGURE 2.8** Customizing the console settings.

## Setting the Time Zone

Next, Sysinstall asks whether you want to set the system's time zone. Select Yes. The next screen will ask whether your system's clock is set to UTC (known also as Coordinated Universal Time, Greenwich Mean Time, and Zulu Time). It probably isn't, so unless you are sure your clock is set to UTC, select No. The next menu asks you to select your region, your country, and other information about where you are located. After you provide Sysinstall with all this information, it shows you a three-letter abbreviation for your time zone and asks whether this abbreviation looks reasonable. If it looks correct, select Yes. If it doesn't, select No. You can always do it again.

## Linux Compatibility

The next question asks whether you would like to enable Linux binary compatibility. If you select Yes, Sysinstall will install a “mini-Linux filesystem” in your /usr partition that includes the Linux share libraries and other necessary programs for Linux to run on FreeBSD. Unless you are sure you will not be running any Linux programs, I suggest you select Yes. This can be a very useful option. (In fact, I wrote much of the manuscript for this book on StarOffice for Linux, which I ran on my FreeBSD workstation.)

> **NOTE**
> Your first thought might be that you don't want to do this. If you worked with emulators under other operating systems, you know how slow they can be. With FreeBSD, however, this is not the case. Linux support in FreeBSD is not done through an emulator but rather is implemented at the kernel level. FreeBSD's Linux support is so good that it runs most Linux applications as fast as native Linux. In fact, FreeBSD will even run some Linux applications faster than Linux itself runs them!

## Configuring the Mouse

FreeBSD comes with a console mouse daemon that allows you to cut and paste text from the console using the mouse. The next question asks whether you have a non-USB mouse attached to your system. If you do, select **Yes**, and you will see the mouse configuration menu (see Figure 2.9). If you plan to use X-Windows (the FreeBSD graphical interface) most of the time, I suggest you skip this option by selecting **Yes** at the prompt and then choosing **Disable** from the next menu. This will allow X-Windows to access the mouse directly.

![](img/48eec858cce7dfb89da36a4d40b7daf3_79_0.png)

**FIGURE 2.9** Configuring the mouse.

Use the menu options to select the type of mouse you have and the port it is connected to. Read the instructions at the top of each menu to help you determine which protocol and port to select.

X-Windows makes use of all three buttons on a standard mouse. If you have a mouse with only two buttons on it, you need to emulate a three-button mouse by telling the mouse driver to interpret the clicking of both buttons at the same time as the third button. You can do this by selecting the **Flags** option on the menu and typing **-3** in the dialog that pops up. Another useful option you might want to put in here is **-r high** to make the pointer move faster or **-r low** if the pointer moves too fast and you want to slow it down. If you need both options, you can use **-3 -r high**, for example.

After you finish configuring the mouse settings, select the **Enable** option to test and run the mouse daemon. If the mouse is set up correctly, you should now be able to move the mouse pointer around on the screen. When you are done testing the mouse, select **Yes** if the mouse worked (note that the mouse still doesn't work in the menu; you still need to use the arrows and the **Tab** key) or choose **No** if it didn't.

You are then returned to the mouse configuration menu. Assuming that the mouse worked, select the **Exit** option.
