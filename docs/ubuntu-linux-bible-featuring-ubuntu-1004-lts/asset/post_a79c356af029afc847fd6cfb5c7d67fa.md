
# Part II: Ubuntu for Desktop Users

define a networked printer that your system can't detect automatically, skip ahead to the section,
"Manually Defining a New Printer."

## Configuring an Existing Printer

You can fine-tune the settings for any printer on your system by selecting the System Administration Printing menu item, right-clicking the icon for the printer, and selecting Properties from the pop-up menu. This displays the configuration options that are available for a specific printer, as shown in Figure 20-2.

## FIGURE 20-2

The Configuration dialog for a specific printer

![](img/1a233c34336fbf5a85d6eb785e401709_763_0.png)

This dialog lists several different configuration options in its left pane. The Settings pane, which is selected by default, enables you to print a test page to verify that your printer is working correctly, identify how the printer is connected to your system, change the printer type if it was recognized incorrectly, and perform any printer-specific tasks that are available, such as cleaning the print heads on inkjet-style printers.

If your printer was recognized incorrectly or if you want to use drivers that come with the printer, click Change beside the Make and Model field to display the "Change Driver" dialog. This dialog is identical to one of the dialog used when configuring a new printer (shown in Figure 20-4 later in this chapter), which is discussed in the next section.

The other configuration options available in this dialog do the following:

- **Policies**: Enable you to control the state of the printer (it is enabled and accepting jobs, and it is shared so that other systems can access it?), general policies such as what happens if a printing error occurs, and banner options that enable you to print cover pages that can precede and follow each print job with various banners, including banners that identify print jobs as Classified or Top Secret so that any spies in your office will know which documents to steal

- **Access Control**: Enables you to configure who can print on that printer, either by disallowing printing by everyone except selected users, or by allowing printing by everyone except for users

- **Printer Options**: Lets you specify the paper size, type of paper being used, the paper tray (manual feed, paper tray, etc.), the level of quality to use and the resolution in which to print, and so on. This dialog also enables you to specify whether you want to print in grayscale or color and, if in color, which color model to use (RGB, CMYK, etc.). I know what you're thinking, but unfortunately this option cannot be used to enable you to print in color on a black-and-white or grayscale printer

- **Job Options**: Lets you set defaults for the number of copies of each document to print, the default font size and margins for generic text documents, the page orientation, number of pages per side, scaling, and so on

- **Ink/Toner Levels**: Provides access to messages that are available regarding printer ink or toner levels and general printer status

After changing any of these options, click OK to save your changes and close this dialog. The main printer configuration utility dialog, shown in Figure 20-3, will still be visible on your screen.

## Manually Defining a New Printer

The dialog shown in Figure 20-3 enables you to configure existing printers or manually add new printers to your system, including shared printers. You can start this utility at any time by selecting the System Administration Printing menu command.

FIGURE 20-3
The Ubuntu Printers dialog

![](img/1a233c34336fbf5a85d6eb785e401709_764_0.png)

# Part II: Ubuntu for Desktop Users

To begin manually defining a new printer, click the Add icon or select Server New Printer to start the Wizard that helps configure a new printer. After the Printers utility processes and parses its database of available printers, the first page of the "New Printer" dialog is displayed, as shown in Figure 20-4.

FIGURE 20-4

Specifying how a new printer is connected

![](img/1a233c34336fbf5a85d6eb785e401709_765_0.png)

This dialog displays various choices for how your system will communicate with the new printer. Depending on the connection mechanism that you select, you should be able to obtain all of the necessary information from the documentation for your printer, from your local system administrator, or by examining your system. The connection options are grouped into two sections, one for locally-attached devices, and one for network devices:

- **Devices**: This section enables you to define printers that are physically connected to your system through one of the following devices:
  - Printer-Name: Identifies a printer that is connected to your system via USB, showing the system's idea of the printer type
  - LPT #1: A printer that is connected to your system's parallel port
  - Serial Port #1: A printer that is connected to the first serial port on your system. Serial printers are extremely uncommon nowadays, but if you are using one, you will need to provide information about your new printer. Enter the communication speed (Baud rate) that your new printer supports, change the type of parity, the number of data bits, and the way in which the printer tells the system to start/stop sending data (Flow Control). The default values (8 data bits, no parity, and one stop bit) are usually the correct settings.
- **Serial Port #2**: A printer that is connected to the second serial port on your system
- **Other**: A local printer that you can access through a Universal Resource Identifier (URI) that uniquely identifies its mechanism
- **Network Printer**: Lists any existing network printers that can be located automatically, and provides several generic types of communicating with:
  - AppSocket/HP JetDirect: A printer that you can print directly over the network by using a specific IP address and port. This is a common way of printing modern standalone printers from manufacturers such as Brother, HP, Epson, and so. After selecting this option, you will need to provide information about your printer. Enter the name or IP address of the printer in the Host field. You can leave the default port (9100) unchanged unless you use a different port for JetDirect.
  - Internet Printing Protocol (IPP): A printer whose queue is managed by a specific host. IPP is a common alternative to JetDirect but supports capabilities such as authentication, access control, and host-side formatting, and you will need to know the name or IP address of the host that manages the printer and the name of the queue for the specified printer on that host. You can use the "Find Queue" button to list all of the publicly available queues on a specified host.
  - LPD/LPR printer: A printer whose queue is managed by a specific host (including the host) using the traditional UNIX Printer Daemon (LPD) protocol. You will need to know the name or IP address of the host that manages the printer, and the name of the queue for the specified printer on that host. You can use the Probe button to list all of the publicly available queues on a specified host.
  - Windows printer via SAMBA: A printer that is managed by a host located on a Microsoft Windows network. Such hosts are typically Windows servers, but can also include Samba servers running on other UNIX or Linux systems on your network. You will need to know the name of your local workgroup or domain, or the IP address of the host that manages the printer, and the name of the queue for the specified printer on that host. You can use the Browse button to navigate through your local workgroup/domain to locate the publicly available queues on a specified host.

Select the mechanism that your system uses to connect to the printer that you are adding, and specify any information that is required to communicate with the printer. Click Forward to proceed to the dialog shown in Figure 20-5.
