
![](img/840007e8f98ea6653e5877e945c27dc6_520_0.png)

**Figure 12-16** The Network address setup screen

- 11. If you're not using DHCP, press Alt+U to clear the Update name servers and search list via DHCP check box.
- 12. Press Tab to select OK and press Enter to return to the Network address setup screen.
- 13. Press Tab to select the Routing option and enter your default gateway configuration.
- 14. As in the graphical version, you can use the Advanced option to set another IP address for your machine or to configure DHCP client options and hardware settings. After finishing the configuration changes, press Tab to select Next and press Enter to return to the Network cards configuration screen.
- 15. Press Tab to select Finish, and press Enter to save your changes and return to the Network Configuration screen.

## Perform Online Updates

After finishing the network card configuration, click or select Next to save your settings and display the Test Internet Connection dialog box. You can conduct a test of your Internet connection or skip the test and continue with the installation. If you select the default option to test your Internet connection, YaST attempts to download the latest release notes and checks for any updates. After the test is finished, a results message is displayed. You can use the View Logs option to view details, and then select Next to continue. If online updates are available, you can download and install them now, or skip the download and continue with the Service Configuration screen shown in Figure 12-17.

![](img/840007e8f98ea6653e5877e945c27dc6_520_1.png)

**Figure 12-17** The Service Configuration screen

The Service Configuration screen contains options to create the certification authority (CA) and configure the LDAP service. The CA Management option is used to configure the CA services for encrypting passwords and other secure data transmissions between server and client. Notice that by default, the Start LDAP Server option is set to No. When configuring a SUSE Linux server for eDirectory, the OpenLDAP server is replaced by the eDirectory service and for most installations should not be used. For a standard OES Linux server installation, you should leave the Service Configuration options unchanged and click or select Next to create the CA certificate and update the system settings.

# Open Enterprise Server Configuration

Next, you have the option to install the Novell Open Enterprise Server configuration. The Open Enterprise Server (OES) configuration includes eDirectory and several Novell services that make the SUSE Linux server perform most of the NetWare services you have studied in previous chapters. The default option is to install the OES configuration now by simply selecting Yes to initialize the eDirectory configuration and display the eDirectory Configuration – New or Existing Tree window. Although you can add the OES Linux server to an existing tree, the default option is to create a new eDirectory tree by entering a unique tree name and then selecting Next to display the Admin user name and password fields. Enter the distinguished name for your administrative account (in this example, cn=Admin.o=AeroDyn) followed by the password you want to use for this account. After retyping the password in the Verify Password field, select Next to display a window for entering the server context and port information (see the text-based YaST screen in Figure 12-18).

![](img/840007e8f98ea6653e5877e945c27dc6_521_0.png)

You should document the default port numbers for future reference, and then select Next to display the NTP and SLP configuration window. As described in Chapter 7, having the same time synchronized on all servers is important for replicating eDirectory changes throughout the network. In the Network Time Protocol field, you can select the local computer clock, or enter a DNS name or IP address of an Internet time server. The Service Location Protocol (SLP) is used to advertise services on an IP-based network so that client computers can locate network resources. On small to medium networks of fewer than 10 servers, you should select the Use multicast to access SLP option so that user agents running on client computers can find services without the need to configure directory agents. After setting the NTP and SLP configurations, select Next to perform the eDirectory configure and start the eDirectory service. This process might take several minutes; when it's finished, you see the release notes.

# Specify Device Configuration Settings

Review the release notes, and then click Next to display the Hardware Configuration window, similar to the text-based version in Figure 12-19.

![](img/840007e8f98ea6653e5877e945c27dc6_522_0.png)

Figure 12-19 The Hardware Configuration screen

In text-based YaST, you can configure display settings by following these steps (or use similar steps in graphical YaST):

- 1. Press Tab to highlight the Change option and press Enter to display a menu with options to change graphics cards, printers, and sound and to reset defaults.
- 2. Press Enter to select the Graphics Cards option and display the SaX2: Extended X11 Configuration dialog box shown in Figure 12-20.

![](img/840007e8f98ea6653e5877e945c27dc6_522_1.png)

Figure 12-20 The SaX2: Extended X11 Configuration dialog box

- 3. Double-click the Desktop icon in the Component list on the left.
- 4. Click the Monitor option to display the Currently configured monitors dialog box showing any currently attached monitors and their settings.
- 5. With your current monitor highlighted, click the Change configuration button and then click Properties to open the xapi dialog box, similar to the one in Figure 12-21.

![](img/840007e8f98ea6653e5877e945c27dc6_523_0.png)

Figure 12-21 Configuring monitor settings

- 6. Notice that this dialog box has tabs to configure frequencies and other export options and the Manufacturer Disk button for inserting a driver utility disk from the monitor manufacturer. In the section on the right, change your settings to a higher resolution (1024 x 768), and then click OK to return to the Currently configured monitors dialog box.
- 7. Click Finish to return to the SaX2: Extended X11 Configuration dialog box.
- 8. Click the Finalize button to open the SaX2 final steps dialog box with options to test, save, or cancel your configuration change.
- 9. Click the Test button to conduct a test of your new configuration settings. If the test displays the new configuration successfully, click Save and then click OK to return to the Hardware Configuration screen.

After making any further hardware configuration changes, select the Next option to configure devices and display the Installation Completed screen shown in Figure 12-22. Select the Finish option to restart your system and display the SUSE Linux login window. You learn more about logging in and working with your SUSE Linux system in the next section.

# Activity 12-1: Performing a SUSE Linux Installation

**Time Required:** 50 minutes

**Objective:** Perform an installation of SUSE Linux Enterprise Server 9.

**Requirements:** A Windows XP computer running VMware Workstation 5 or a computer with at least 256 MB RAM and 5 GB free hard drive space (4 GB for the SUSE Linux OS and 1GB unpartitioned space) and the SUSE Linux CD-ROM DVD) or CD. This activity assumes a blank hard drive with no other operating systems installed.

**Description:** To take advantage of open-source software options and reduce licensing costs, UAS is planning to use SUSE Linux servers. In this activity, you perform an installation of SUSE Linux Enterprise Server 9 using a dual-boot computer or VMware. If you’re using VMware, use the text-based installation and then configure your monitor for 1024 x 768 resolution.

![](img/840007e8f98ea6653e5877e945c27dc6_524_0.png)

Figure 12-22 The Installation Completed screen

- 1. If you’re using VMware, create a new virtual computer for the SUSE Linux server as described in Appendix C. If you’re using a dual-boot computer, you should have Windows XP Professional installed and have at least 5 GB of unpartitioned space on your hard drive.
- 2. Insert the Installation CD 1 into the CD-ROM drive, and restart your computer or start your virtual machine. After a short time, the SUSE Welcome screen and installation options are displayed.

![](img/840007e8f98ea6653e5877e945c27dc6_524_1.png)

> If you’re using VMware, click in the SUSE Linux window to pass keyboard and mouse control to your virtual Linux environment.

- 3. Press **Tab** to stop the 20-second timer.

![](img/840007e8f98ea6653e5877e945c27dc6_524_2.png)

> The VMware video environment might not be recognized by the SUSE graphical environment, which can cause an error message or an unreadable screen. If this happens, restart your virtual machine. When the Welcome window is displayed, click in the window, and then press F2 and select the Text Mode installation option.

- 4. From the installation menu, select **Installation** (and press **Enter**, if you’re using the text-based installation) to display the license agreement screen. In the Novell Software License Agreement screen, select **I Agree** to display the installation language selection screen.
- 5. Verify that English is selected, and then select **Accept** to display the installation options.

![](img/840007e8f98ea6653e5877e945c27dc6_524_3.png)

> If you’re using the text-based installation mode, press Tab to select an option and then press Enter instead of clicking an option button. You can also press Alt with the option’s highlighted letter to select it. If you’re using the graphical interface, your screens will be slightly different.

- 6. If necessary, select **New Installation** and then select **OK**. After a short detection process, the Installation Settings screen is displayed.
