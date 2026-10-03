
If you cannot find a terminfo entry for your printer, you can try selecting a similar type of printer; however, you might have trouble keeping the printer set in the correct modes for each print request. If no terminfo entry exists for your type of printer, and you want to keep the printer set in the correct modes, you can either customize the interface program used with the printer or add an entry to the terminfo database. You'll find the printer interface program located under the /etc/lp/interfaces directory. Editing an interface file or adding an entry to the terminfo database is beyond the scope of this Training Guide. A printer entry in the terminfo database contains and defines hundreds of items. Refer to the Solaris 8 System Administration Guide, Volume II in the Answerbook2 online manuals for information on performing this task. Another good reference on this topic is John Strang and Tim O'Reilly's book “termcap & terminfo” published by O'Reilly & Associates, Inc. (ISBN: 0937175226).

## ADMINISTERING PRINTERS

Managing the print system involves monitoring the lp system and uncovering reasons why it might not be working properly. Other routine tasks involve canceling print jobs and enabling or disabling a printer while it's being serviced. This section provides instructions for the daily tasks you will perform to manage printers and the print scheduler. All of the following commands require superuser access.

## Deleting Printers and Managing Printer Access

Use Admintool to delete a printer from the system. In the Print Manager window of Admintool, highlight the printer you want to delete and select Edit, Delete, as shown in Figure 10.6. The printer queue will be deleted from the system.

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_430_0.png)

FIGURE 10.6
Deleting a printer.

To delete a printer at the command line, issue the following command on the system where the printer is connected:

```
lpadmin -x <printer-name>
```

The printer is deleted from the system.

Perhaps you do not want to remove the printer from the print server, but you want to keep a particular system from printing to the print server. Issue the following command on the print client from which you want to delete the printer:

```
lpsystem -r <print-server>
```

The print server is deleted from the print client's /etc/lp/Systems file.

Perhaps a printer will be going offline for repairs. To stop accepting print requests on a particular printer, type the following command on the system where the printer is physically connected:

```
reject <printer-name>
```

This step prevents any new requests from entering the printer's queue while you are in the process of removing the printer.

To allow a printer to keep taking requests, but to stop the printer from printing the requests, type the following command on the system where the printer is physically connected:

```
disable <printer-name>
```

When stopping or disabling a printer, you might need to move existing jobs that have been queued to that printer. To move print jobs from one printer to another, use the lpmove command as follows:

```
lpmove <printer1> <printer2>
```

The arguments for the lpmove command are described in Table 10.4.

## TABLE 10.4

### lpmove ARGUMENTS

| Argument | Description |
|---|---|
| `<printer1>` | The name of the printer from which all print requests will be moved. |
| `<printer2>` | The name of the printer to which all print requests will be moved. |

If you move all the print requests to another printer, the lpmove command automatically stops accepting print requests for printer1. This next step is necessary if you want to begin accepting new print requests for the printer:

```
accept printer1
```

In the following example, the lpmove command moves print requests from the printer eps1 to the printer eps2, for example, when eps1 is being taken down for maintenance. After the printer is ready to start accepting print jobs again, use the accept command to resume accepting print requests on eps1:

```
lpmove eps1 eps2
accept eps1
```

## Creating Printer Classes

You can put several locally attached printers into a group called a printer class. This might be helpful if you have several printers sitting next to each other, and it doesn't matter which printer your job goes to. When you have set up a printer class, users can then specify the class (rather than individual printers) as the destination for a print request. The first printer in the class that is free to print is used. The result is faster turnaround because all printers are utilized. You create printer classes with the lpadmin command as follows:

```
lpadmin -c
```

No default printer classes are known to the print service; printer classes exist only if you define them. Following are three ways you can define printer classes:

- By printer type (for example, PostScript)
- By location (for example, 5th floor)
- By work group or department (for example, Accounting)

Alternatively, a class might contain several printers that are used in a particular order. The LP print service always checks for an available printer in the order in which printers were added to a class. Therefore, if you want a high-speed printer to be accessed first, you would add it to the class before you add a low-speed printer. As a result, the high-speed printer would handle as many print requests as possible. The low-speed printer would be reserved as a backup printer when the high-speed printer was in use.

Printer class names must be unique and can contain a maximum of 14 alphanumeric characters and underscores. You are not obligated to define printer classes. You should add them only if you determine that using printer classes would benefit the users on the network.

## STEP BY STEP

## 10.2 Defining Printer Classes

To define a printer class, follow these steps:

- 1. Log in as superuser or lp on the print server.
- 2. Define a class of printers by using the lpadmin command:
  `lpadmin -p <printer-name> -c <printer-class>`

The arguments for lpadmin are described in Table 10.5.

## TABLE 10.5

### lpadmin ARGUMENTS

| Argument | Description |
|---|---|
| `-p <printer-name>` | The name of the printer you are adding to a class of printers |
| `-c <printer-class>` | The name of a class of printers |

The specified printer is added to the end of the list in the class in the print server's /etc/lp/classes/<printer-class> file. If the printer class does not exist, it is created. Verify the printers in a printer class by using the lpstat command:

```
lpstat -c printer-class
```

In the following example, the command adds the printer luna to the class roughdrafts:

```
lpadmin -p luna -c roughdrafts
```

## Checking Printer Status

The lpstat command is used to verify the status of a printer. You can use this command to determine which printers are available for use or to examine the characteristics of a particular printer. The lpstat command syntax is as follows:

```
lpstat [-d] [-p <printer-name> [-D] [-l]] [-t]
```

The lpstat command options are described in Table 10.6.

## TABLE 10.6

### lpstat Command Syntax and Options

| Option | Description |
|---|---|
| -a | Reports whether printers are accepting requests. You can also specify a specific list of printers, as shown in the example `lpstat -a eps1 eps2 eps3`. |
| -d | Shows the system's default printer. |
| -p <printer-name> | Shows whether a printer is active or idle, when it was enabled or disabled, and whether it is accepting print requests. You can specify multiple printer names with this command. Use a space or a comma to separate printer names. If you use spaces, enclose the list of printer names in quotes. If you don't specify the printer name, the status of all printers is displayed. |
| -D | Shows the description of the specified printer. |
| -l | Shows the characteristics of the specified printer. |
| -t | Shows status information about the LP print service, including the status of all printers—whether they are active and whether they are accepting print requests. |
| -u <logon-IDs> | Print the status of output requests for users, in which <logon-IDs> can be one or all of the following:
  - `<user>` A user on the local system, as shown in the example `lpstat -u bcal...`
  - `<host!user>` A user on a system, as shown in the example `lpstat -u systema!bcal...`
  - `<host!all>` All users on a particular system, as shown in the example `lpstat -u systema!all`
  - `<all!user>` A particular user on all systems, as shown in the example `lpstat -u all!bcal...`
  - `all` All users on all systems specified as follows: `lpstat -u all` |
