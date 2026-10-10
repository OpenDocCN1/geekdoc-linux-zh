
![](img/eff8b9287a5f38c5adf538f24aacf29e_730_0.png)

**Figure 11-44** *Peripheral Devices Window*

The two *Action* menu picks here are *Zoom* and *Show Device Files*. Selecting *Zoom* produces a window with such information as hardware path, driver, description, and status. The devices files associated with the item you have highlighted will be shown if you select Show Device Files.

Disks and File Systems was covered earlier in this chapter.

Instruments may appear if your system supports HP-IB cards.

Printers and Plotters is covered later in this chapter.

## Tape Drives

Tape Drives lists the tape drives connected to your system. You are shown the Hardware Path, Driver, and Description for each tape drive. You can add, remove, diagnose tape drives, list tape drive device files, and add new tape drive device files. Figure 11-45 shows a four-drive DLT unit attached to the system:

![](img/eff8b9287a5f38c5adf538f24aacf29e_731_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_732_0.png)

**Figure 11-45** Tape Drives Window

## Terminals and Modems

Your system’s terminals and modems are listed for you when you enter this subarea. You can perform a variety of tasks from the Actions menu, including the following:

- Add Terminal or Modem
- Remove Terminal or Modem Port
- Lock Terminal or Modem Port
- Unlock Terminal or Modem Port
- Modify Terminal Security Policies
- Modify Terminal Authorized Users
- Additional Information

## Uninterruptable Power Supplies

Your system’s uninterruptable power supplies are listed for you when you enter this area, including the UPS type, device file of the UPS, hardware path, port number, and whether or not shutdown is enabled. The *Actions* you can select are: *Modify Global Configuration*, Add, Zoom, Remove, and Modify.

## Printers and Plotters

*Printers and Plotters* is divided into two subareas: *HP Distributed Print Service* and *LP Spooler*. *HP Distributed Print Service (HPDPS)* is part of the Distributed Computing Environment (DCE). It is not covered in this book. *LP Spooler* is covered in this section; Figure 11-46 shows the hierarchy of *Printers and Plotters*:

- Printers and Plotters
  - HP Distributed Print Services
  - LP Spooler
  - Print Requests
    - **Actions:**
      - Stop or Start Print Spooler
      - Zoom
      - Cancel Request
  - Printers and Plotters
    - **Actions:**
      - Add Local/Printer Plotter
      - Add Remote Printer/Plotter
      - Add Network-Based Printer/Plotter
      - Stop or Start Print Spooler
      - Show Common Problems
      - Zoom
      - Remove
      - Enable or Disable
      - Accept or Reject Requests
      - Modify Fence Priority
      - Set as System Default Destination
      - Show Member of Class
      - Save/Restore Spooler Config
    - **Actions:**
      - Save Spooler Configuration
      - Restore Spooler Configuration
      - Zoom

![](img/eff8b9287a5f38c5adf538f24aacf29e_734_0.png)

**Figure 11-46** *Printers and Plotters* Menu Structure

## Print Requests

Under *Print Requests*, you can manage the print spooler and specific print jobs. You can start or stop the print spooler and cancel print jobs. The following information on print requests is listed for you:

- **Request ID:** An ID is associated with each print job. This is the Printer Name followed by a number.
- **Owner:** The name of the user who requested the print job.
- **Priority:** The priority of a print job is assigned when the job is submitted. The *p* option of `lp` can be used to assign a priority to a job. Each print destination has a default priority that is assigned to jobs when *p* is not used on the `lp` command.
- **File:** The name of the file sent to the print queue.
- **Size:** The size of the print job in bytes.

The *Actions* menu allows you to act on print jobs by cancelling them. In addition, the print spooler can be stopped and started.

You can configure both local and remote printers in *Printers and Plotters*. When you select *Add Local Printer/Plotter* from the *Actions* menu and then the appropriate type of printer, a window is opened for you in which you can supply the specifics about the printer. Before this window is opened, however, you must specify whether the *type* of printer to be added is: parallel; serial; HP-IB; non-standard device file; or a printer connected to a TSM terminal, as well as to which I/O card to add the printer. One huge advantage to adding the printer using SAM is that this process is entirely menu-driven, so you only have to select from among the information that is supplied.

The window appears to ask you for the following information:

- **Printer Name**
  You can pick any name for the printer. I usually like to use a name that is somewhat descriptive, such as *ljet5* for a LaserJet 5. The name is limited to 14 alphanumeric characters and underscores.
- **Printer Model/Interface**
  SAM supplies a list of all interface models for you when this window is opened. These models are located in the `/usr/lib/lp/model` directory. Each printer has an interface program that is used by the spooler to send a print job to the printer. When an interface model is selected, the model is copied to `/etc/lp/interface/<printername>`, where it becomes the printer’s interface program. Models can be used without modification, or you can create customized interface programs.
- **Printer Class**
  You can define a group of printers to be in a class, which means that print requests won't go to a specific printer but will go to the first available printer within the class. This is optional.
- **Default Request Priority**
  This defines the default priority level of all requests sent to this printer.
- **Default Destination**
  Users who do not specify a printer when requesting a print job will have the print request sent to the default printer.

You could use SAM to view printers or you could use the lpstat command showing printers configured on a system as shown in the following example:

```bash
$ /usr/bin/lpstat -t
scheduler is running
system default destination: ljet5
members of class laserjet:
ljet5
device for ljet5: /dev/cltd0_lq
ljet5 accepting requests since Nov 21 22:45
printer ljet5 is idle, enabled since Nov 21 22:45
fence priority: 0
no entries
```

As with all the other tasks SAM helps you with, you can manage printers and plotters manually or you can use SAM. Not only does SAM make this easier for you, but I have also had nothing but good results having SAM do this for me. As you go through the SAM Log file, you will see a variety of lp commands that were issued. Some of the more common commands, including the lpstat command issued earlier, are listed in Table 11-2:

## Table 11-2 lp Commands

| Command | Description |
| :--- | :--- |
| `/usr/sbin/accept` | Start accepting jobs to be queued. |
| `/usr/bin/cancel` | Cancel a print job that is queued. |
| `/usr/bin/disable` | Disable a device for printing. |
| `/usr/bin/enable` | Enable a device for printing. |
| `/usr/sbin/lpfence` | Set minimum priority for spooled file to be printed. |
| `/usr/bin/lp` | Queue a job or jobs for printing. |
| `/usr/sbin/lpadmin` | Configure the printing system with the options provided. |
| `/usr/sbin/lpmove` | Move printing jobs from one device to another. |
| `/usr/sbin/lpsched` | Start the **lp** scheduling daemon. |
| `/usr/sbin/lpshut` | Stop the **lp** scheduling daemon. |
| `/usr/sbin/lpstat` | Show the status of printing based on the options provided. |
| `/usr/sbin/reject` | Stop accepting jobs to be queued. |

## Save/Restore Spooler Configuration

Occasionally, the spooler can get into an inconsistent state (usually, something else has to go wrong with your system that ends up somehow changing or renaming some of the spooler configuration files). SAM keeps a saved version of the spooler’s configuration each time it is used to make a change (only the most recent one is saved). This saved configuration can be restored by SAM to recover from the spooler having gotten into an inconsistent state. Your latest configuration is automatically saved by SAM, provided that you used SAM to create the configuration, as opposed to issuing **lp** commands at the command line, and it can be restored with *Restore Spooler Configuration* from *Save/Restore Spooler Config*. This screen allows you to save your current spooler configuration or restore a previously saved spooler configuration information.
