
- Add drivers from the workstation you are running Novell iManager from by selecting **Add** from System.
  The drivers installed on your workstation are made available for upload to the Driver Store.
  You can upload only drivers for the same platform as the workstation.

- 4. Select the driver you want; then select **OK**.
- 5. Save your changes by selecting **OK**.

![](img/9129877170834ca9d5fdac5319bf5f12_455_0.png)

You can also install driver files from a terminal prompt using the `iprntcmd` command.
For details, see “Using iprntcmd on Linux and Macintosh,” on page 37 in the Novell OES iPrint Administration Guide for Linux.
You can access the guide from http://www.novell.com/documentation/oes or from the OES_Docs directory on your 3086 Course DVD 2.

## Create a DNS Name for the Print Manager

The Print Manager creates a URL for each printer based on the Print Manager configuration.
When you create the Print Manager, you can specify an IP address or DNS name for the Novell iPrint Service.
You should always use a DNS name because using an IP address forces users to delete and reinstall printers if the IP address changes.

## Set Up and Configure the Print Manager

The Print Manager provides a platform where Printer Agents can reside on the server. Printer Agents are representations of actual printers. When a print job is submitted to the Print Manager, the print job is forwarded to a printer when the printer is ready.
To set up and configure the Print Manager, do the following:

- Create a Print Manager
- Start the Print Manager

### Create a Print Manager

You need to create at least one Print Manager for your print system; depending on your network setup, you can create additional Print Managers (for example, across a WAN link).
The Print Manager must be running to create printers.
A Driver Store must exist before you create a Print Manager.
To create a Print Manager, do the following:

- 1. Make sure you have configured a DNS name for the Print Manager.
- 2. From Novell iManager (on the left), select **iPrint > Create Print Manager**.
- 3. Fill in the appropriate fields.
  To view explanations about the fields, select Help.
- 4. Make sure the **Start Print Manager after Creation** check box is selected.

If you do not select this option, you have to start the Print Manager by using **Manage Print Manager > Manager Control** in Novell iManager or by entering `/etc/init.d/novell-ipsmd start` at a shell prompt.

- 5. When you finish, select **OK**.
  After the Driver Store is created and the daemon is loaded on the server, you can start adding printer drivers.

## Start the Print Manager

From Novell iManager, on the Print Manager Control Property page, you can view the Print Manager’s status and unload or load the Print Manager daemon.

You do the following:

- 1. From Novell iManager, select **iPrint > Manage Print Manager**.
- 2. Browse to and select the Print Manager you want to manage.
  See Figure 12-27 for what should appear.

![](img/9129877170834ca9d5fdac5319bf5f12_456_0.png)

**Figure 12-27**

- 3. Start the Print Manager by selecting **Manager Control > Startup**. (To stop the Print Manager, select **Manager Control > Shutdown**.)
- 4. Select **OK**.

## Create Printers

After you have created a Print Manager, you can create a printer by doing the following:

- 1. From Novell iManager (on the left), select **iPrint > Create Printer**.
- 2. Follow the prompts and fill in the fields.
  You can view explanations about the fields by selecting Help.
- 3. When you finish, select Next; then select the drivers for this printer.

![](img/9129877170834ca9d5fdac5319bf5f12_457_0.png)

If the printer drivers for this printer are not listed, you can still create the printer.

After the printer is created, add the printer drivers to the Driver Store, and then associate the drivers to the printer by selecting **Manage Printer > Drivers**.

- 4. When you finish, create the printer by selecting Next.

## Manage Printers

Although the default settings let users print without additional configuration, you might want to modify some of those settings so that you can manage your printing resources more effectively.

You can modify the settings by doing the following:

- Create Additional Printers
- Manage Printer Agents
- Use Printer Driver Profiles
- Enable Novell iPrint Direct
- Manage Print Jobs

## Create Additional Printers

Before creating additional printers, ensure you meet the following prerequisites:

- Have the Supervisor right to the destination container where its associated Printer object is to reside.
- Be designated as a manager of the Print Manager that controls this printer.
- Have a Driver Store running.
- Have a Print Manager running.

To create additional printers, do the following:

- 1. From Novell iManager, select **iPrint > Create Printer**.
  See Figure 12-28 for what should appear.

![](img/9129877170834ca9d5fdac5319bf5f12_458_0.png)

Figure 12-28

- 2. Fill in the fields.
  Select Help for explanations about the fields.
- 3. Select OK.
- 4. Select Next.
  See Figure 12-29 for what should appear.

![](img/9129877170834ca9d5fdac5319bf5f12_458_1.png)

Figure 12-29

- 5. Select the *drivers* for this printer.
  If the printer drivers for this printer are not listed, you can still create the printer.
  After the printer is created, you can add the printer drivers to the Driver Store and then associate the drivers to the printer by selecting **Manage Printer > Drivers**.

These drivers are automatically downloaded to users’ workstations when they install the printer in the future.

Because the list of printer drivers included with this product is limited, you can add drivers to the Driver Store.

If you do not select a driver, users are prompted to provide a disk with the appropriate driver the first time they install this printer on their workstations.

- 6. Create the printer by selecting **Next**.

## Manage Printer Agents

Using Novell iManager, you can manage Printer Agents. You can start up and shut down a Printer Agent, pause and resume input and output, view printer information, change configuration settings, and change the printer drivers.

Do the following:

- 1. From Novell iManager, select **iPrint > Manage Printer**.
- 2. Browse to and select the *printer* you want to manage.
  See Figure 12-30 for what should appear.

![](img/9129877170834ca9d5fdac5319bf5f12_459_0.png)

Figure 12-30

- 3. Use the tabbed property pages (or drop-down list in Firefox) to complete the appropriate task.

## Use Printer Driver Profiles

Printer driver profiles let you set the driver defaults for a Windows printer driver. Then you associate the printer driver profile to a printer so that when the printer is installed, it is configured with the settings you want.

For example, in a law office you might want the default paper size to be legal size. This means every time the printer and corresponding driver are installed on a workstation, the paper size is set to legal size.

To use printer driver profiles, you need to know how to do the following:

- Create, Modify, and Delete a Printer Driver Profile
- Associate a Printer Driver Profile with a Printer

### Create, Modify, and Delete a Printer Driver Profile

When creating a printer driver profile, you work directly with a platform-specific printer driver. For this reason, you need to create and modify profiles from the same operating system platform as the printer driver.

For example, to create or modify a Windows 2000 printer driver profile, you must access Novell iManager and complete the task from a Windows 2000 workstation.

Do the following:

- 1. From Novell iManager, select **iPrint > Printer Driver Profile**.
- 2. Browse to and select the *Print Manager* where you want the driver profile stored and made available to the printers on that manager.
- 3. Select one of the following:
  - *Create Printer Driver Profile*—Creates a new printer driver profile.
  - *Delete Printer Driver Profile*—Deletes an existing printer driver profile.
  - *Modify Printer Driver Profile*—Changes the settings of an existing printer driver profile.
- 4. Select OK.

### Associate a Printer Driver Profile with a Printer

After creating a printer driver profile, you need to associate it with a printer. Do the following:

- 1. From Novell iManager, select **iPrint > Manage Printer**.
- 2. Browse to and select the *printer* you want to modify.
- 3. Select **Drivers >** *printer_driver_operating_system*.
- 4. From the list of Available Drivers, select the printer driver.
- 5. From the list of Available Driver Profiles for Selected Driver, select the *profile* you want associated with this printer.
  If you do not want a profile associated, select None.
- 6. Save the changes by selecting OK.

## Enable Novell iPrint Direct

Users of a Novell iPrint Direct-enabled printer send print jobs directly to the printer instead of sending jobs to the Print Manager first. The job is sent to the printer in LPR or raw 9100 format, depending on the setting gateway autoload command for the printer.

![](img/9129877170834ca9d5fdac5319bf5f12_460_0.png)
