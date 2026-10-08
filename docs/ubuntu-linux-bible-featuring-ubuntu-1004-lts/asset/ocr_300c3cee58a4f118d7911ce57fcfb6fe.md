# Chapter 20: Adding Hardware and Attaching Peripherals

To verify that your printer definition is correct, a dialog that asks if you want to print a test page displays:

+   - To print a test page, click Yes. After attempting to print a test page, this displays the configuration dialog shown in Figure 20-3, which enables you to make changes if any are necessary. If the test page prints correctly, click Cancel to close this dialog. If the test page did not print correctly, change the configuration of your printer and try again. Once the test page prints correctly, click OK to save the updated configuration information for your printer.
- If you don't want to print a test page at the moment, click No.

The dialog shown earlier in Figure 20-3 displays showing an icon for the new printer. The default printer for a system is indicated by a green checkmark on its icon. To change the default printer for your system, right-click its icon and select Set as Default from the pop-up menu. This displays a dialog asking if you want to make the selected printer the default printer for all users (system-wide default), or your personal default printer.

To test a printer at any time, right-click its name, and select Properties from the pop-up menu. This displays a Properties dialog like the one shown in Figure 20-3. To verify that your printer is working correctly, click "Print a Test Page." This queues and prints a test page for your printer. If the test page does not print use the other sections of the Properties dialog to verify that the correct settings are used and that the printer manufacturer and driver for your printer are specified. You should then be able to print a test page successfully.

# Tip

If your printer is not automatically detected or cannot be made to print with any manual setting specified in the "Add printer" dialog, try rebooting your system with the printer connected and turned on. In some rare cases, Ubuntu's printer and device subsystems may not correctly detect a device unless it is present and active when you boot your system.■

# Using a Scanner

Modern scanners are USB devices and are well supported on Linux systems, as older scanners that use a real SCSI (Small Computer System Interface) interface. Scanners are supported on Linux systems through the SANE (Scanner Access Now Easy) interface and associated front-end and back-end applications. The home of the SANE project is www.sane-project.org. If you are still shopping for a scanner or are interested in whether support for a specific scanner is available under Linux, see the page at www.sane-project.org/sane-supported-devices.html, which also provides access to an easy-to-use search engine application that provides data about specific scanners.

Ubuntu offers two main scanning packages, both of which use the SANE drivers:

+   - Simple Scan: as the name suggests, a fast, easy-to-use scanning package that is suitable for most basic scanning needs. This scanning package is automatically installed on Ubuntu systems.