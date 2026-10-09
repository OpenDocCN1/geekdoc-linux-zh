
To show all of the *supported* printer devices, which are listed in the ODM predefined database, use the following command:

```
# lsdev -Pc printer
...
printer opp    parall0  Other parallel printer
printer osp    rs232    Other serial printer
printer osp    rs422    Other serial printer
printer hp1j-4 parall1  Hewlett-Packard LaserJet 4,4M
printer hp1j-4 rs232    Hewlett-Packard LaserJet 4,4M
printer hp1j-4 rs422    Hewlett-Packard Laserjet 4,4M
...
```

The output of both of the *lsdev* commands will vary, depending on how many printers are configured and which printer drivers have been installed on the system. You can ignore *printer* device attributes, since they are not used in printing through either AIX or System V subsystems. If the printer device driver is not currently installed on your system, you can install it using the SMIT *FastPath smit install_package*. To install an individual printer device, you can do a search of the installation CD-ROM by typing a forward slash, /, and entering the search pattern for the printer you want to add. Normally, it is not necessary to have an exact match between the printer driver and the printer model. For example, you can use the HP Laserjet II Printer driver for most HP printers. An exact match may give you extra functionality, so I always try to match the driver to the printer model.

Once the printer driver is installed, you can proceed to add the System V printer to the system. There are three steps to enable the printer. The **lpadmin** command is used to add the printer:

```
# mkdev -c printer -t hp4V -s parall1 -p ppae0 -w p
# lpadmin -p hp4V -v /dev/lp0 -d "Hewlett-Packard LaserJet 4,4M"
```

After the System V printer has been added to the system, you need to use the **accept** command to allow the printer to accept print requests:

```
# accept hp4V
```

The last step is to enable the new print queue using the **enable** command:

```
# enable hp4V
```

If you prefer using the *printer wizard*, you can use the Web-Based System Manager, WebSM. Start WebSM using the **wsm** command. From the main screen on the left side, select *Printers (System V)*. Then select **Standard Overview And Tasks**. In the middle of the screen, select **New Printer** and fill in each field and the printer wizard will do everything for you, including allowing the printer to accept requests and enabling the queue. Figure 12-14 shows the WebSM menu for System V printer subsystem.

![](img/82f851021955589d82b22750fb3b1646_280_0.png)

Figure 12-14. Main System V printer window for WebSM

## Adding a Network System V Printer

Adding a network printer involves a few more steps than adding a local printer. You have to perform most of the following steps:

- Register each of the remote systems.
- Allow or deny user access.
- Set the parameters for the remote system.
- Configure the remote client.
- Define the print queue on the remote client.

To register the remote system with the System V print service, use the following command syntax:

```
# lpsystem [-T timeout] [-r retry_attempts] <system_name>
```

To define the print queue on the remote client, use the following command syntax:

```
# lpadmin -p <client_printer_name> -s <remote_pr_server>:<remote_pr_queue>
```

After this step, be sure to **accept** and **enable** the print queue on the remote client.

To grant or deny user access to the remote printer, use the following command syntax:

```
# lpadmin -p <printer> -u allow:AIX_user_list
# lpadmin -p <printer> -u deny:AIX_user_list
# lpsstat -p -l             The lpched daemon must be running!
```

## Managing System V Printers

Plenty of Administrative System V printer commands are available to accomplish any task. The **lpadmin** command can do most of the tasks you want to do when you select the appropriate command parameter. All the System V administrative commands are listed in Table 12-6.

| System V Command | Duties Performed |
| :--- | :--- |
| accept | Allows the printer to accept print requests for the specified destination. The destination can be a printer or a class of printers. |
| reject | Stops all print queuing to the specified destination. |
| enable | Activates the specified print queue by enabling the queue to print requests queued by the **lp** command. For remote print queues, the **enable** command will allow the transfer of the request only to the remote print server. |
| disable | Disables all print requests from printing on the specified queue. |
| lpadmin | Allows you to add, remove, and change printers, as well as set default destinations, set up alerts, and define remote printers. |
| lpfilters | Used to add, delete, change, and list filters used with the **lp** print service. |
| lpforms | Used to provide administration for preprinted forms. |
| lpmove | Provides a mechanism to move print requests between printers and queues. |
| lpsched | The System V print service master control. |
| lpshut | Stops the System V print service. |
| lpsystem | Defines network parameters to the System V print service. |
| lpusers | Sets limits on the queuing priority levels for jobs submitted by users. |

**Table 12-6.** System V Print Services Administration Commands

## Using Forms with System V Print Service

Using forms with the System V print service has seven possible steps. These are registering the form with the print service, requesting a form for a print job, alerting the user to mount the form in the printer, mounting the form, unmounting the form, controlling who can access the form, and displaying status information. Each of these steps is outlined in the following sections.

### Registering a Form with the Print Service

A form needs a form definition file, which describes the form. Things like number of pages, character pitch, and page length and width need to be defined. Once you have created the form definition, register it with the System V print service using the following syntax:

```
# lpforms -f <form_name> -F <form_definition_file>
```

### Requesting a Form to Submit a Print Job

A user can request a specific form by using the lp -f command using the following syntax:

```
# lp -f <form_name> -d <printer> <file_to_print>
```

The previous command will queue the print job, but the form must be mounted before the job will print.

### Alerting Someone to Mount a Form

Before the job can print on the specified form, the form must be mounted. This is usually done by an operator or a print services administrator. To set up print services to notify the Print Services Operator when a user has requested a form, use the following syntax:

```
# lpforms -f <form_name> -A <alert_type> [-Q number] [-w interval]
```

where:

- **-f form_name** is the name of the specific form.
- **-A alert_type** can be either mail, write to the console, shell_script to run, quiet to stop messages, or none for no alert.
- **-Q number** starts alerting when number of form requests have been queued. The default is one.
- **-w interval** defines the number of minutes between resending the alert. The default is zero.

### Procedure to Mount a Form

The following five steps are needed to let the print services know that the form is mounted:

1. Disable the print queue using the **disable `<print_queue>`** command.
2. Load the form into the printer.
3. Tell the print services that the form is mounted and ready to print on using the following command syntax:
   `# lpadmin -P <printer> -M -f <form_name>`
4. Align the form if necessary.
5. Enable the printer using the **enable `<print_queue>`** command.

### Unmounting a Form From the Printer

The following four steps are necessary to unmount a form from the printer and inform the print service that the form is no longer mounted:

1. Disable the printer using the **disable `<print_queue>`** command.
2. Unload the form from the printer.
3. Tell the print service that the form is no longer available using the following command syntax:
   `# lpadmin -p <print_queue> -M -f none`
4. Reenable the print queue using the **enable `<print_queue>`** command.

### Limiting Access to Forms

If you want to limit who can print on your expensive preprinted forms, you can use the following commands:

```
# lpforms -f <form_name> -u allow:AIX_user_list
# lpforms -f <form_name> -u deny:AIX_user_list
```

where **AIX_user_list** is a list of AIX users separated by commas.

### Gathering Form Information

The following command is used to gather information about a particular form:

```
# lpforms -f <form_name> -l
```

The output of this command will vary, depending on who is running the command. The **root** or **lp** user will see the complete picture including the user allow and deny lists.
