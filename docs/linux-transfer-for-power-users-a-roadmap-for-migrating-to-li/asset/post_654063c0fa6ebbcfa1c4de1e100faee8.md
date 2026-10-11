
In order to assign a static IP address to a specific Ethernet interface, highlight the interface of interest in the Network Devices list box, and click the Edit button in the upper right corner of Figure 29 to open the Edit Interface dialog, shown in Figure 73.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_85_0.png)

Figure 73. Use the Edit Interface dialog to assign a static IP address to a computer's Ethernet card.

You can use this dialog to enter data for the specific Ethernet interface that was highlighted in the Network Configuration screen (you can see this behind the Edit Interface dialog in Figure 73). That's why the title bar of the dialog identifies the name of the device.

First, uncheck the "Configure using DHCP" check box. Doing so will enable the IP Address and Netmask text boxes below.

Second, enter the static IP address you want to assign to the Ethernet interface, and the netmask of the device as well. See Figure 74 for an example.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_86_0.png)

Figure 74. Entering the static IP address for an Ethernet interface.

Finally, click OK to get back to the Network Configuration screen, as shown in Figure 75.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_86_1.png)

Figure 75. The Network Configuration screen, ready for a manually entered hostname.

The next step is to assign a name to the machine you're working on, instead of letting the machine get a name automatically assigned to it (via DHCP). Click the "manually" option button in the Hostname area. Doing so enables both the Hostname text box and all of the text boxes under the Miscellaneous Settings label.

Enter a hostname for the machine. You can enter simply a label, as shown in Figure 76, or enter a fully qualified hostname (as shown in the example on the screen: host.domain.com).

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_87_0.png)

Figure 76. A manually entered hostname and gateway address.

You can also enter the IP address for the gateway machine on your network (such as the IP address of your router) and the IP addresses for your DNS servers.

Then click the Next button, and you're all done with setting static IP addresses.

### Network Configuration

Any network devices you have on the system will be automatically detected by the installation program and shown in the Network Devices list.

To configure the network device, first select the device and then click Edit. In the Edit Interface screen, you can choose to have the IP and Network information configured by DHCP or you can enter it manually. You can also choose to make the device active at boot time.

If you do not have DHCP client access or are unsure as to which this information is, release the DHCP lease and configure manually.

## Summary

Desktop Linux is ready for power users. Installing Fedora Core on a PC is an easy task in 2004. FC recognizes a great deal of hardware, and the wizard’s user interface is as smooth and bug-free as I’ve encountered in the Linux world. While some of the terminology may need a bit more work before I’d turn it over to a complete novice, the installation is definitely ready for prime time as far as power users go.

The purpose of this chapter is to get you started with Linux on your desktop, but of course there’s a lot more than what I can cover here. In addition, new versions of Fedora Core are released on a regular basis. I’ll keep you up to date by writing new articles as well as posting updates related to this book. These materials can be found on Hentzenwerke’s Web site, www.hentzenwerke.com. Click “Catalog” and navigate to the page for Linux Transfer for Windows Power Users.

## Chapter 3: Updating Fedora Core

Unless you're installing a brand-new version of a piece of software, there are bound to be updates available for it, and Fedora Core is no exception. Updating your system with the latest patches, bug fixes, and security updates will keep your system running as smoothly and problem-free as possible. Because Fedora Core is Linux, there's not just one way to update your system. In this chapter, I’ll explain how the Fedora Core basic update process works and how to use the various mechanisms available to you.

Updating a piece of software has become a nearly trivial process. In the olden days, many software manufacturers didn’t automatically issue patches and updates. Instead, they rolled fixes into an update or upgrade that may or may not have been free. You had to wait for patch disks to show up in the mail, or, worse, had to request the disks after a chance discovery of their availability.

Once bulletin boards became more widespread, and communication software and hardware advanced sufficiently, some manufacturers posted patch files on their boards, or on third-party boards like CompuServe, and posted announcements about their availability on various electronic forums.

After Web sites made their debut in the early '90s, companies began migrating their patches and updates to a company support site, and started using e-mail to notify users of availability as well.

Still, it was up to the user to be proactive enough to get and install the updates. This wasn’t always easy, and a combination of lack of sophistication on the part of some users as well as less-than-coherent directions from the software company made this all too often a risky procedure.

Nowadays, it’s become common for software to “phone home” to the manufacturer in order to check on whether or not updates are available, and, if so, alert the user. Some software can be configured to look for and install updates automatically, without any user intervention. Whether or not you take advantage of this capability is up to you. Many users of Windows systems configure their anti-virus products to go through automatic updates, but don’t let the operating system get patched automatically, due to the irregular quality of service packs and other patches.

Fedora Core does the first part—checking to see if updates are available and notifying the user—via the Red Hat Network Alert Notification Tool, which appears as an icon in the panel, as shown in Figure 1.

When the machine can connect to the Internet, it will attempt to query a Web site for information about available updates. When the icon is green, it means that FC is currently querying for updates, as shown in Figure 2.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_89_0.png)

Figure 1. Upon startup, the Red Hat Network Alert Notification Tool displays a blue check mark that indicates it is not aware of any new updates.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_89_1.png)

Figure 2. The Red Hat Network Alert Notification Tool icon's green color means updates are currently being queried.

If there are updates available that have not been applied, the icon turns red, as shown in Figure 3.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_89_2.png)

Figure 3. The round red icon in the lower right corner of the panel indicates that updates are available.

After all available updates have been applied, the icon turns blue again, meaning that the system is up to date, as shown in Figure 4.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_89_3.png)

Figure 4. The blue check mark indicates that no updates are available.

If you move your mouse over the icon, a tooltip will display how many updates are available and how many have been ignored during the last update session. If the tooltip in Figure 3 alarms you (nearly 100 updates available), remember that there could be thousands of packages installed on an FC system. Furthermore, the more time that has passed since the time when the ISOs you used to install were made available and the last update session, the more updates will be available. If you install FC (or any distro, for that matter) with old files, there will likely be a lot of updates to install the first time you do an update, but significantly fewer each successive update.

Fedora Core provides three mechanisms to upgrade your system. Before I get into the specific mechanisms, a word about three items: dependencies, RPMs, and the Red Hat Network.

### Dependencies

No man is an island, nor are too many pieces of software. Many applications aren't monolithic files, but instead rely on other files or applications. For example, in order to run application A, application B must be installed as well. This requirement is called a "dependency" (in that A is dependent on B).

The core Linux operating system, as with all operating systems, consists of hundreds and hundreds of files—and if you include the applications that come with most distros, you're looking at thousands of files. Many of them have dependencies—including multiple dependencies. For example, A depends on B and C. B depends on D, which depends on E, and C depends on F. In order to install A, then, you have to install B, C, D, E, and F. Given that other programs also have intertwined dependencies, you can see how the whole situation can get confusing quickly.

In the olden days, you had to resolve these dependencies by hand. Not appealing. What people would do, then, is write scripts (think "batch files" or "macros") that would automate these processes. Much better. But still a nuisance.

So Red Hat created the Red Hat Package Manager, intended to provide a clean front end to the scripts that automated the dependency problem.

### RPMs

RPM is short for "Red Hat Package Manager." It's a tool that automates much of the process of installing and uninstalling parts of an FC system. The RPM tool has several pieces.

The first is a database on your own system that contains information about packages and the files required by each package. When you install or uninstall packages, RPM tracks this information in the database. Suppose you install a package that uses File A. Later, you install a second package that also uses File A. Because File A was installed with the first package, it's not installed again. If you later uninstall the first package, File A is not removed, because it's still needed by the second package. All of this is handled by RPM.

The second piece of the RPM tool is software that provides a variety of functions that work with this database, such as installation, uninstallation, and information about the contents of a package, what is currently installed, and so on.

The third piece is the RPM package itself. Every RPM has two files, a header file and the package file. The header contains a list of all files, descriptions of the packages, requirement and conflict lists, and some other descriptive information. Different update mechanisms use the RPM database on your system and the RPM headers in different ways.

Fedora Core is not the only Linux distribution using the RPM system. Obviously, Red Hat's corporate offerings use it, but so do SuSE and others.

Installing an RPM package is as simple as issuing this command:

```
rpm -i abc.1386.rpm
```

If the installation succeeds, no output will be returned. You can use the -ivh parameters to provide verbose feedback on the installation.
