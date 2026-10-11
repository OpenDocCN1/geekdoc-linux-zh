
## 3. Select the printer manufacturer, or the location of the PPD file.

CUPS uses standard PostScript Printer Description (PPD) files to handle formatting print for printers. These use the same concept as the standard printer drivers for Microsoft Windows you're probably used to. Each printer must have a PPD installed for CUPS to know how to format text and graphics sent to the printer.

This wizard window allows you to select the PPD file to use for the new printer. You have three choices:

- Select the printer manufacturer from the list of installed drivers.
- Select to install your own provided PPD file for the printer.
- Search the Internet for a PPD file to download.

If you're lucky enough to have the PPD file for your printer, copy it to a location on your Linux system and select the Provide PPD file option. Browse to the location of the file and select it, and then click Forward.

If you don't have the PPD file for your printer, you can try to search the standard repositories for one. If you find the printer manufacturer listed, select it and click Forward.

## 4. If you selected a printer manufacturer, the next wizard window provides a list of specific printer models and PPD files. Select the printer model and (optionally) the proper PPD file.

This wizard window asks you to select the specific model type for your printer. Hopefully your printer model is listed. If not, you must go back a step and find your own PPD file to install.

If your specific model is listed, select it, and a list of available PPD files is shown. Some models may only have one PPD file, but others may have two or more files to choose from. In that case, one is usually marked as recommended. Try that first: If it doesn't work, select a different PPD file. Clicking the Forward button takes you to the final wizard window.

## 5. Create a unique name for the printer, and optionally enter a description and location. Click Apply on the summary window to create the new printer.

The new printer is added to the list of local printers (even if you mapped to a remote printer). You should now see the new printer when printing from applications on your system. Before getting too carried away with your printing, it's a good idea to check how the printer is configured.

### Modifying printer properties

You can modify the properties of any printer on the system (whether Linux automatically created it or you manually created it). Click the gear icon next to the printer and a content menu with four options appears.

### Printer Options

The Printer Options dialog box allows you to set some properties for the physical printer setup. The properties available for you to modify are based on information provided by the individual printer's PPD file and depend on the physical characteristics of the printer.

These properties are divided into separate categories, depending on the printer's capabilities. The options available for my test printer are shown in Figure 17-11.

![](img/577d3bff979ee86b07f9836e0df274ce_352_0.png)

FIGURE 17-11: The Printer Options area of the Printer Configuration tool.

The Page Setup settings handle properties such as what types of paper the printer can handle, the print qualities it can produce, and the number and types of input trays. You can force the printer server to request a specific paper size for all print jobs, or even request which paper tray to take paper from.

The Installable Options settings set the specific features provided by the printer, such as custom page sizes or duplex printing.

### Printer Details

The Printer Details area provides some basic settings you can change for the printer. From here, you can change the description and location tags for the printer, the URL of the printer, and the PPD file used for the printer.

### Use Printer by Default

Most applications allow you to select a printer to use if you have more than one printer configured. However, some applications don't allow you to do that, or assume there's a default printer. Selecting this option sets this printer as the default printer for the system.

### Remove Printer

Removes the printer definition from the CUPS server. This also removes any queues created for the printer so no printer jobs can be processed.

### System Monitor

Although things usually go well on Linux systems, sometimes applications can go awry. When that happens, it's handy to be able to watch what's going on under the hood of the operating system.

The System Monitor tool provides information about how the system hardware and software are working. It's often included by Linux distributions to provide a graphical peek at your system. Both Ubuntu and openSUSE include this feature by default.

To start the System Monitor tool in Ubuntu, from the application launcher click the System Monitor icon, or enter it in the Search text box. In openSUSE, from the Applications menu select System and click the System Monitor icon. While there are some differences between the System Monitor tool in Ubuntu and openSUSE, they both provide much the same information. To save space I just walk through the System Monitor as it appears in Ubuntu.

There are three window tabs in the System Monitor:

- Processes: Shows information about programs currently running on the system
- Resources: Shows information about CPU and memory usage.
- Filesystem: Shows information about what hard drives are mounted on the system

Of course, just having a bunch of information thrown at you doesn't help at all. You need to know what that information means for it to be meaningful. The following sections help you understand how to interpret the various pieces of information contained in the System Monitor.

### Processes

Clicking the Processes tab provides an overview of the programs currently running on the system, as shown in Figure 17-12.

![](img/577d3bff979ee86b07f9836e0df274ce_354_0.png)

**Processes** — the Linux term for programs running on the system — are shown in a table format. The default view shows all the processes that are currently being run by your user account. Alternatively, you can watch all the processes, or just the ones that are actively working, by clicking the menu icon in the title bar and selecting which option you want to view.

You can sort the table rows based on any of the table columns. For example, to see what processes are using the largest percent of CPU time, click the % CPU column heading. The System Monitor automatically sorts the rows based on percentage of CPU usage.

Other columns are available for you to add. Choose Menu Preferences to see the options available for the Processes tab. Table 17-2 lists the data available to display in the Processes tab.

#### TABLE 17-2 System Monitor Process Table Columns

| Column | Description |
| :--- | :--- |
| Process Name | The program name of the running process |
| User | The owner of the process |
| Status | The status (either sleeping or running) of the process |
| Virtual Memory | The amount of virtual system memory allocated for the process |
| Resident Memory | The amount of physical memory allocated for the process |
| Shared Memory | The amount of memory shared between this process and other processes |
| %CPU | The percentage of total CPU time the process is using |
| CPU Time | The actual CPU time the process is using |
| Started | The time the process started running |
| Nice | The system priority of the process; higher nice numbers have lower priority on the system |
| ID | The unique process ID (PID) the system assigned to the process |
| Command Line | The name of the command and any command line arguments used to start it |
| Memory | The amount of system memory the process is using |
| Waiting Channel | The channel the process is waiting in |
| Control Group | The kernel control group the process belongs to |
| Unit | The systemd startup unit the process belongs to |
| Session | Additional details about the process session |
| Seat | The terminal the process was launched from |
| Owner | The userid that started the process |
| Disk read total | Total bytes read by the process |
| Disk write total | Total bytes written by the process |
| Disk read | Bytes read by the process since the last update |
| Disk write | Bytes written by the process since the last update |
| Priority | The system priority assigned to the process |

You can set a few other options while you're in the Preferences dialog box:

- Update Interval in Seconds: How frequently the System Monitor refreshes the table data
- Enable Smooth Refresh: Gathers new process information before refreshing the table data, instead of refreshing table data as it gathers process information
