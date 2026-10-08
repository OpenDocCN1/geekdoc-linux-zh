![](bbox=[0.17, 0.11, 0.83, 0.44])

**FIGURE 4-3** The system-config-printer tool

To add a new printer, click **New Printer**. To edit an installed printer, click its entry in the Server Settings pane to display its configuration panels. There are panels for Settings, Policies, Access Control, Printer Options, and Job Control. Once you have made your changes, you can click **Apply** to save your changes and restart the printer daemon. If you have more than one printer on your system, you can make one the default by clicking **Make Default Printer** button in its Settings panel. The **Delete** button will remove a printer configuration. You can test your printer with a PostScript, A4, or ASCII test sheet selected from the Test menu.

# New Printers

When you click **New Printer**, a series of dialog boxes are displayed where you can enter the printer name, its type, and its model. In the Printer Name dialog box, give the printer a name along with any particular description.

On the following Select Connection screen, you select the appropriate printer connection information. Connected local printer brands will be listed by name, such as Canon, whereas for remote printers you specify the type of network connection, like Windows printers via Samba for printers connected to a Windows system, or Internet Printing Protocol (**ipp**) for printers connected to other Linux systems, or AppSocket/HP Direct for HP printers connected directly to your network.

For most connected printers, your connection is usually determined by the device hotplug services udev and HAL, which now manage all devices. This will be the first entry