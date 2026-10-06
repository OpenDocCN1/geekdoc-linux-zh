
# Chapter 10 ♦ Running SUSE Linux

![](img/a2d958d7eab32ca5b89b2b8af808aa70_360_0.png)

Figure 10-2: Use the arrow and Tab keys to navigate YaST in text mode.

YaST offers you some intuitive tools for configuring your system and also preconfigured so you start with a nice set of defaults. YaST also does a good job detecting your hardware, finding partitions, and the like, so a new user can just accept the settings YaST chooses. Here are some examples of what YaST does for you:

- **Detects hardware**— You don't have to check /etc configuration files or run lshmod to see how your hardware has been configured in SUSE. From the Hardware section, you can select icons representing your CD drives, graphics cards, printers, joysticks, scanners, cards, and mice. Click the Hardware information icon to see your full list of detected hardware.

- **Manages system configuration**— Like Red Hat Enterprise Linux, SUSE stores much of the information it uses to configure services at boot time in the /etc/sysconfig directory. The information in those files is in the form VARIABLE="VALUE"

Under the YaST icon, you can select the sysconfig Editor, which lets you select each file and view and possibly change each variable so you don't have to guess what variables are available for each configuration. For more advanced system administrators, this is a great way to fine-tune the startup services for your system.

SUSE also includes a System Profile Management (SCPM) applet, which lets you store and manage a collection of system settings so it can be used after days.

- **Configures network devices**— YaST detects your dial-up modem, Ethernet card, DSL modem, or IS hardware, and gives you the opportunity to configure each piece of hardware. SUSE also does a much better job than Winmods working in Linux, which is particularly useful for using dial-up features on laptops that have cheap, built-in modems.

- **Defines network services**— With a connection to a LAN or WAN, YaST provides some helpful graphical tools for configuring some services that can be unintuitive from the command line.

- **Changes security settings**— Security settings in Linux are often among the most unintuitive features to configure, while at the same time being among the most important. Although features such as iptables work well for most Linux gurus for setting up a firewall, people who are accustomed to graphical interfaces may find them challenging.

From the YaST Security and Users selection, the Firewall icon enables you to step through your network interfaces and add access to those services you want by name (as Web Server, Mail Server, and Other Services) or by port number. It enables you to do initial setup of most complex firewall features, such as forwarding, IP Masquerading, and logging.

Make your way around the graphical YaST interface, you need only to click the mouse and use the Tab key to move between fields. For the text-based YaST interface, you can use the Tab and arrow keys to move among the selections and the Enter key to select the currently highlighted item.

# RPM Package Management

Like Hat Linux, SUSE packages its software using the RPM package management format and related tools. RPM contains a lot of features for adding, removing, and managing software in SUSE. Although software packages in the Red Hat and SUSE distributions are different, the tools you use for managing packages in those two are similar.

You use the rpm utility to work with RPM packages. Here's a list of its features:

- **Installing local or remote packages**— You can use the rpm command to add a software package to SUSE, and rpm doesn't care if the package is in the local directory, CD, or remote computing (providing you have network access to that computer). A remote package can be available on a web server (http://) or FTP server (ftp://). Here is an example of using rpm command to install a software package from an FTP server:

```
# rpm -iv ftp://ftp.linuxxt.net/pub/suse/10.0/abc.i586.rpm
```

In this example, the -i option allows to install the package, and the -v option says to give verbose output as the output. The fictitious package (abc.i586.rpm) is installed from an FTP repository. If there are dependency or access issues, rpm informs you and fails. Otherwise, the package is installed. The -U option is used instead of the -i option to install RPMs because -U succeeds if the package is already installed. The -U says to

- **Querying the RPM database**— One of the best features of the RPM facility is that you can find out a lot of information about the software packages that are installed. The query option (-q) lets you list package names, descriptions, and contents in various ways. Here are a few examples:

```
# rpm -qa xmms less
# rpm -ql xmms less
# rpm -qi xmms less
```

The first example (-q) searches for the xmms package and reports the current version of the package that is installed. In the second, -ql lists all files in the xmms package and pipes that to the less command to go through it. Finally, -qi displays a description and other information about the xmms package.

- **Verifying installed packages**— Use rpm to verify the contents of an RPM package. The -v option enables to check whether any of the files in a package have been tampered with. Here is an example:

```
# rpm -V aaa_base
....5 c /etc/inittab
S....5 T /etc/profile.d/alias.ash
```

-V checks any of the contents of the aaa_base package (which contains some system configuration files) have been modified. The output shows that the initab and alias.ash files have been modified from the originals. The 5 indicates that the timestamp on the file differs. On the alias.ash file, the 5 shows the size of the file differs.

The rpm command has many other options as well. To find out more about them, type man rpm from any.

# Automated Software Updates

As version 7.1, SUSE Linux includes an automatic update agent. YaST Online (YOU) is built right into the YaST facility and offers an easy way to get updates, security patches, and fixes for SUSE by downloading and installing them from repositories over the network.

From Yaast, select YOU. YOU shows the location of mirror sites and then enables you to begin retrieving software updates with a single click. It presents you with a list of patches from which you can choose. Security patches are in red, recommended patches are selected, and optional patches are (unselected). After you have secured the updates you want and clicked OK, you can watch the progress as each patch is downloaded and installed. Having security-related patches and other fixes separated and the ability to read all software update on the YaST window set YOU apart from methods of doing upgrades from other distributions.

# Getting Support for SUSE

SUSE has an excellent support database and full-time support staff. You can search many of the articles on the site for free. Paid support options are available as well.

The SUSE Linux Portal (http://portal.suse.com) is the place to search for answers using SUSE. You don't need a user account to search articles related to Linux, although you do need to search articles related to business products from SUSE. To get an account, select the Sign Up from the SUSE Linux Portal. If you have purchased your SUSE product, you can use that account to register your SUSE product. Having a registered SUSE product lets you use your account to get free installation information and other support services.

With the split of OpenSUSE and SUSE Linux, look for many of SUSE's online resources to be divided as well. For example, SUSE resources are already being directed to Novell.com or OpenSUSE.org If you are learning or choosing OpenSUSE as your entry into Linux products, you should start at the OpenSUSE.org site for information on downloads, documentation, and communications opportunities (mailing lists, forums, IRC, and so on).

> At the time of this writing, SUSE is offering a free 30-day evaluation for SUSE Linux Enterprise Server if you want to download it. That evaluation includes support and upgrade protection. Check the Novell (www.novell.com) and SUSE (www.suse.com) Web sites if any evaluation are currently available.

# Installing OpenSUSE

The SUSE installation procedure described here is for OpenSUSE Linux 10.0. This edition is available for free. Functionally, it is almost the same as the SUSE Linux 10.0 boxed set version that Novell sells. The primary differences between the two are product support (only with SUSE Linux) and inclusion of some non-open source software (also only with SUSE Linux). So, essentially, these instructions should work equally well for both SUSE and OpenSUSE 10.0.
