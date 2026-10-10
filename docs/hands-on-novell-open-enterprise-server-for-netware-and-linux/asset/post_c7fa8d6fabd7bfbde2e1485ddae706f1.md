
## DOWNLOADING AND INSTALLING SUSE LINUX

As of this writing, SUSE Linux 10 is the latest version of the SUSE Linux operating system offered by Novell. The product includes the stable, secure Linux kernel plus a complete set of desktop applications, including an office suite, the Mozilla Firefox Web browser, an instant messaging client, multimedia viewers, and graphical software. You can obtain SUSE Linux 10 directly from Novell's Web site (www.novell.com/products/suselinux) by selecting the free download or Buy SUSE Linux 10 options. SUSE Linux 10 currently costs less than $60 and comes on a bootable CD. The purchased product includes printed documentation plus 90 days of installation support.

Novell also has its own customized version of SUSE Linux called Novell Linux Desktop (NLD). As of this writing, it's based on SUSE Linux 9 and is available at http://download.novell.com/Download?buildid=IMABtBtXadQ~. You can buy the full version for $35 or download a free 60-day trial version. Novell Linux Desktop includes a customized KDE desktop with utilities and options such as the Novell Client for Linux that make it easier to adapt to a Novell-based network environment. If you're using Novell Linux Desktop, you'll notice minor differences in the desktop environment and certain system utilities, such as YaST.

![](img/840007e8f98ea6653e5877e945c27dc6_607_0.png)

> **NOTE**
> Novell Linux Desktop is also available in a preloaded virtual machine format that can be run directly from VMware without performing a new installation. See Appendix C for more information on using VMware.

### Installing SUSE Linux 10

The process for installing SUSE Linux 10 is similar to installing the OES Linux Enterprise Server 9 as explained in Chapter 12. If you're using VMware, create a virtual machine for the SUSE Linux operating system as described in Appendix C. The following steps summarize the process of installing a SUSE Linux 10 system that you can use to perform the activities in this book and appendix:

1. Boot your system from the SUSE Linux 10 CD. Accept the default language, accept the license agreement, and set your time zone.
2. Select the KDE desktop from the Desktop selection window to display the Installation settings window.
3. Click the Software link to display the Selections window (see Figure B-1).

![](img/840007e8f98ea6653e5877e945c27dc6_607_1.png)

**Figure B-1 The SUSE Linux 10 Selections window**

4. Click the Network and Server check box in the left pane, and then click the ncpfs (Tools for Accessing Novell File Systems) option in the Package section.
5. Follow these steps to add software packages for supporting Novell Client for Linux:
    - a. Click the Filter list arrow and click Search in the list of options.
    - b. Enter gcc in the Search text box and click the Search button.
    - c. Click to select the gcc (the GNU C Compiler and Support Files) option.
    - d. Enter kernel-default in the Search text box and click the Search button.
    - e. Click to select kernel-default (the standard kernel) and respond to the warning by clicking OK.
    - f. Click Accept to accept your changes, and then click Continue to respond to the Changed Packages message box and return to the Installation Settings window.
6. Click Accept to accept the installation settings and then click to confirm any license agreements.
7. Click Install when you see the Confirm Installation window.
8. After files are copied, you’re prompted to restart to continue the installation.
9. Insert the SUSE Linux CDs and click OK when prompted.
10. After all files have been copied, you’re asked to enter a password for your root user. Enter a password of at least eight characters containing both uppercase and lowercase letters. Write down the password and keep it in a secure place.
11. Click Next to display the Network Configuration window.
12. Click the Network Interfaces heading and then click Edit to display the Network Address Setup window shown in Figure B-2.

![](img/840007e8f98ea6653e5877e945c27dc6_608_0.png)

13. Depending on your lab environment, select automatic or static address setup. If you click Static Address Setup, enter the IP address and subnet mask your instructor provides.
14. Click the Host Name and Name Server button to display the Host Name and Domain Name window.
15. Enter a name for your Linux computer in the Hostname text box and a domain name in the Domain Name text box.
16. If you’re using a DNS server in your lab, enter its IP address in the Name Server 1 text box, and then click OK to return to the Network Address Setup window.
17. Click Next to save your settings and return to the Network Configuration window.
18. Click Next to save the network configuration and display the Test Internet Connection window.
19. If your computer is attached to the Internet, click Next to test your connection. If not, click the No, Skip This Test option button, and then click Next to display the Authentication Method window.
20. Verify that the Local (/etc/passwd) option button is selected, and then click Next to display the New Local User window.
21. Create a new user for yourself by filling in the fields shown in Figure B-3. Click Next to create your user account and display the SUSE Linux 10 Release Notes.

![](img/840007e8f98ea6653e5877e945c27dc6_609_0.png)

Figure B-3 The New Local User window

22. Read the notes and click Next to display the Hardware Configuration window.
23. Verify that the correct graphics card is configured, and then click Next to save the hardware configuration.
24. Click Finish to complete your installation and display the SUSE Linux 10 login window.

### Using the Novell Linux Desktop Virtual Machine

The Novell Linux Desktop virtual machine is a convenient way to run SUSE Linux from VMware: First you need a copy of VMware Workstation or VMware Player (described in Appendix C), and then you install VMware on your computer. Next, you need to download a copy of Novell Linux for Desktop (the nld9_vmwarews5-vm.zip file from www.novell.com/downloads). After you’ve downloaded the file, you can use the following steps to install it:

1. Click Novell Linux Desktop in the Product or Technology (optional) drop-down list, and click Search to display the products list.
2. Click the Novell Linux Desktop SP2 Evaluation product to display a list of files.
3. Click the nld9_vmwarews5-vm.zip file and log in to the Novell site. (You might be asked to create a user account at that time.)
4. Click the Download option and save the file to your local computer’s hard disk.
5. Extract the file to your Virtual Machine folder.

![](img/840007e8f98ea6653e5877e945c27dc6_609_1.png)

The installation instructions for Novell Linux Desktop are at www.novell.com/documentation/nld/esd/gplnld9-eval.html. You need to follow them carefully to use VMware and the supplied NLD 9 distribution.

After you have downloaded the VMware Workstation 5 Virtual Machine for Novell Linux Desktop 9, unzip the file (nld9-vmwares5-vm.zip) to the directory on your Linux or Windows system where you keep your virtual machines. By default, it’s home/username in Linux and My Documents\My Virtual Machines in Windows. When unzipping the file, make sure you re-create the folders in the .zip file.

Next, start VMware Workstation 5, open the virtual machine, and then power it on. At this point, you see a message asking whether you want to create a new identifier or keep the existing one. Keeping the existing identifier is strongly recommended. If you don’t, you’ll need to reconfigure the network card in the virtual machine.

In some circumstances, the X-Window system fails to initialize correctly on the virtual machine. If this happens, you see a text-based console repeated four times on the screen. To fix the problem, follow these steps:

1. Log in as root with the password “novell” (all lowercase letters).
2. Change to run level 3 by typing init 3 and pressing Enter.
3. Reset the X Server by typing sax2 -r and pressing Enter.
4. When the configuration screen prompts you to accept the configuration or change it, press OK to accept.
5. In the text-based console, start the X-Window system by typing init 5 and pressing Enter, or restart the system by typing init 6 and pressing Enter.

## Using SUSE Linux to Perform Administrative Tasks

Because Novell OES enables you to perform administrative tasks in iManager and Remote Manager via a Web browser, you can work in both SUSE Linux 10 and Windows XP. SUSE Linux 10 includes the Mozilla Firefox Web browser, which has been used to test chapter activities. The activities in the book that can be done with the Firefox Web browser are identified in the requirements section for each activity. This section describes how to access iManager and Remote Manager using the Mozilla Firefox Web browser and points out any differences you might notice when using Firefox instead of Internet Explorer.

### Starting iManager and Remote Manager

To start iManager or Remote Manager via SUSE Linux 10 Mozilla Firefox, you need to know the IP address or DNS name of your OES NetWare or Linux server. You can use these steps to start either utility from your Firefox Web browser:

1. Start the Firefox Web browser. If you’re not connected to the Internet, you might see a message stating that www.novell.com could not be found. If so, click OK to display the Firefox window shown in Figure B-4.
2. Enter https://IPaddress/nps/iManager.html (for iManager) or https://IPaddress:8009 (for Remote Manager) in the text box next to the home icon, and press Enter to open a secure connection.
3. Because Firefox doesn’t recognize the certificate the OES server uses to establish a secure connection with SSL, you see the message box shown in Figure B-5.
4. To avoid seeing this message in the future, click the Accept this certificate permanently option button and click OK to continue. If you’re using an IP address to access the OES server and the OES server has a DNS name defined, you see the Domain Name Mismatch error message (see Figure B-6).
5. If you like, click the View Certificate button to view the server’s certificate, and then click OK to continue and display the login window. You can then log in to iManager or Remote Manager to perform administrative functions.
