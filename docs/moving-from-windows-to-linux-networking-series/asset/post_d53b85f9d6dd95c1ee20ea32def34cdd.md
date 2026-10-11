
![](img/12d790664598bbf390261087fbe55bbc_132_0.png)

Before we can discuss the security settings, it would be prudent to have a brief introduction to how networks and the Internet communicate. In short, data is broken down into packets that are sent using various protocols. A protocol is simply a standardized way of communicating. There are a number of protocols used in networks and on the Internet, each with its own purpose. It is not necessary for a casual home user to memorize these, but since some readers might be their office system administrators, the most commonly used protocols are described in Table 6.1.

**Table 6.1: Protocols**

| Protocol | Description |
| :--- | :--- |
| HTTP | This is Hypertext Transfer Protocol. It is the protocol used by Web browsers such as Netscape Navigator and Mozilla to communicate with Web servers and display Web pages. |
| FTP | File Transfer Protocol. This protocol is used to upload and download files. If you have ever downloaded a demo game, music, or any file from the Internet, it was probably done with FTP. |
| SMTP | This is Simple Mail Transfer Protocol and is used to send e-mails. |
| POP3 | This is Post Office Protocol, which is used to retrieve incoming e-mails from an e-mail server. |
| DHCP | Dynamic Host Configuration Protocol is used to get an IP address from a server. |

Notice that the Trusted Devices category includes your machine’s own network cards. If you select a device as a trusted device, that means that packets from that device will not be screened. You should think very hard before selecting any device as trusted. As you learn a little more about how networks work, you might consider customizing your security settings.

## Adding and Removing Applications

From time to time you may find that you don’t use an application that you have installed, and you may want to remove it to free up more space on your hard drive. You may discover that you forgot to install some application. The Add and Remove Applications screen, found under System Tools, is what you need for either task. You may recall that in Chapter 2 you were told that if you forgot any applications, they could be installed later. This utility is how you go about doing that.

When you first launch this utility, it will take several moments to load. This is because it is checking your system to see what applications are already installed. While it is loading, you will see a screen giving you the status of the process. This screen is shown in Figure 6.11.

![](img/12d790664598bbf390261087fbe55bbc_133_0.png)

**Figure 6.11** : Checking System Package Status.

Once the utility is loaded, you will have a list of all possible packages that you might install. Applications that are already installed on your system will have a checkmark beside them. Items that are not installed will not have the checkmark. You may check the packages you would like to install and uncheck packages you want to uninstall or remove. Then simply click the **Update** button. Depending on the choices you made, it might take several minutes to add and remove various applications. Also, if you chose to add applications, you will be prompted to insert the appropriate installation disks. You can see the utility's main screen in Figure 6.12a.

![](img/12d790664598bbf390261087fbe55bbc_133_1.png)

**Figure 6.12A** : Adding and removing applications.

### KDiskFree

KDiskFree, shown in Figure 6.12b, is a rather simple utility. It shows you various drives, including floppy and CD-ROM, as well as hard drives. In the display it will show how much space is still free, what percentage is in use, and the Linux device name and initial size of the storage device.

![](img/12d790664598bbf390261087fbe55bbc_134_0.png)

**Figure 6.12B:** KDiskFree.

## Using the KDE Control Center

The Control Center is found on the main Start menu. It is, as the name implies, a centralized location from which to control many important features of KDE. When you first launch the Control Center, you will see something much like what is shown in Figure 6.13. In the main screen on the right side, you should notice that it is telling you what version of KDE you are using, what user account is currently logged in, what operating system you are using (Linux or Unix), and what version of that operating system you are using. The release is the version of the Linux kernel that you are using.

![](img/12d790664598bbf390261087fbe55bbc_135_0.png)

**Figure 6.13:** The Control Center.

On the left side you should see three tables. The first, entitled Index, is a listing of all of the various items you can control through the Control Center. The second tab is a Search tab allowing you to search for a particular item. The third is a Help tab where you can look up help on various KDE topics.

Many of the items you can control from the Control Center are items we previously covered. Things such as appearance and themes, Internet and network, and desktop are all items that we explored previously. The Control Center provides a convenient single location from which to work with many of the various configuration utilities available with KDE. We will not cover the items we have previously examined. They work exactly the same way from the Control Center as they did previously. However, we will look at a few interesting items in the Control Center that we did not examine previously.

### Power Control

If you look under Power Control and select Display Power Control, you will see something much like what is displayed in Figure 6.14. The settings shown here allow you to conserve energy. You can tell your PC to suspend operation after a certain amount of time or to completely power off after a given amount of time. That way, if you walk away from your PC and leave it running, it will eventually shut itself off.

![](img/12d790664598bbf390261087fbe55bbc_136_0.png)

Figure 6.14: Power Control settings.

There is also a Laptop Battery section that is specifically for laptop users. This section enables you to determine how to warn the user if his laptop battery is getting low. If you are installing Linux on a laptop, you would be very wise to set up your laptop battery settings. This screen is shown in Figure 6.15.

![](img/12d790664598bbf390261087fbe55bbc_136_1.png)

Figure 6.15: Laptop Battery settings.

The first tab establishes whether or not to display a battery status icon and how often to check the status of the battery. The second tab is very much like the Power Control settings we previously examined. It allows you to shut down the system power after a given amount of time. You can have a different amount of time selected, depending on whether your laptop is plugged into an outlet or running off battery power. This is a very useful setting and can prevent you from leaving your laptop running and running down your battery. The final two tabs determine how and when the user will be warned about a low battery. If you are using Linux on a laptop, it would be a mistake for you not to become familiar with these settings and to ensure that they are set up in such a manner as to maximize your use of the Linux operating system and your laptop.

## System Administration

You may have noticed a section entitled System Administration. This section is for some of the more common system administration tasks. We will take a look at the ones that are most likely to be of use to you on a routine basis.

## Login Manager

The Login Manager allows you to establish how the login screen is presented to the user when he logs in. This screen has six tabs that enable you to specify every aspect of the login process and appearance. You can see the screen in Figure 6.16.

![](img/12d790664598bbf390261087fbe55bbc_138_0.png)

The first tab allows you to set the greeting, whether or not to show the logo (Tux the penguin), to show a clock, and what color scheme to use for the login screen. You can also change what character appears when someone is typing in a password. Most people are used to seeing one asterisk appear for each character they type, so it's probably a good idea to stick with this format, but you can change it if you want. The next two tabs allow you to further customize the login screen by setting the font and the background. These tabs handle purely cosmetic properties of the login screen and should be set to whatever you find pleasing.

The fourth tab, labeled Sessions and shown in Figure 6.17, is not cosmetic at all. This tab deals with the options the user will be presented with when he gets to the logon screen and what he can do from this screen.
