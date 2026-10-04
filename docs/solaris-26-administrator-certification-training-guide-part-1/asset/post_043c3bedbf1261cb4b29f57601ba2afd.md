
To delete a printer at the command line, issue the following command on the system where the printer is connected:

```
lpadmin -x <printer-name>
```

The printer is deleted from the system.

Maybe you do not want to remove the printer from the print server but you want to keep a particular system from printing to the print server. Issue the following command on the print client from which you want to delete the printer:

```
lpsystem -r <print-server>
```

The print server is deleted from the print client's /etc/lp/Systems file.

Perhaps a printer will be going offline for repairs. To stop accepting print requests on a particular printer, type the following command on the system where the printer is physically connected:

```
reject <printer-name>
```

This step prevents any new requests from entering the printer's queue while you are in the process of removing the printer.

To allow a printer to keep taking requests but to stop the printer from printing the requests, type the following command on the system where the printer is physically connected:

```
disable <printer-name>
```

## Checking Printer Status

The lpstat command is used to verify the status of a printer. You can use this command to determine which printers are available for use or to examine the characteristics of a particular printer. The lpstat command syntax and options are described in Table 9-5.

Table 9-5 lpstat Command Syntax and Options

lpstat [-d] [-p printer-name [-D] [-l]] [-t]

- **-d**: Shows the system's default printer.
- **-p <printer-name>**: Shows if a printer is active or idle, when it was enabled or disabled, and whether it is accepting print requests. You can specify multiple printer names with this command. Use a space or a comma to separate printer names. If you use spaces, enclose the list of printer names in quotes. If you don't specify the printer name, the status of all printers is displayed.
- **-D**: Shows the description of the specified printer.

### Table 9-5 lpstat Command Syntax and Options (continued)

| Option | Description |
|---|---|
| lpstat [-d] [-p printer-name [-D] [-l] [-t]] |  |
| -l | Shows the characteristics of the specified printer. |
| -t | Shows status information about the LP print service, including the status of all printers—whether they are active and whether they are accepting print requests. |

Here are a few examples of the lpstat command:

```
lpstat -p hplaser
```

The system responds with

```
printer hplaser is idle. enabled since Jun 16 10:09 1998. available.
```

In the following example, the command requests a description of the printers hplaser1 and hplaser2.

```
lpstat -p "hplaser1 hplaser2" -D
printer hplaser1 faulted. enabled since Jun 16 10:00 1998. available.
unable to print: paper misfeed jam

Description: Printer by finance.
printer hplaser2 is idle. enabled since Jun 16 10:09 1998. available.
Description: Printer in computer room.
```

In the following example, the command requests the characteristics of the printer hplaser.

```
lpstat -p hplaser -l
printer hplaser is idle. enabled since Jun 16 10:11 1998.
available.
Content types: any
Printer types: unknown
Description: Printer by computer room.
Users allowed:
(all)
Forms allowed:
(none)
Banner not required
Character sets:
(none)
Default is pitch:
Default page size:
```

## Restarting the Print Scheduler

The print scheduler, lpsched, handles print requests on print servers. If prints are not coming out of the printer, you might need to restart the print scheduler. To restart the print scheduler,

you use the lpsched command. If a print request was printing when the print scheduler stopped running, that request will be printed in its entirety when you restart the print scheduler.

First, stop the scheduler by typing

```
/usr/lib/lp/lpshut
```

To restart the scheduler, type

```
/usr/lib/lp/lpsched
```

## Setting a User's Default Printer

When you added the printer, you were given the option of selecting that printer as the default printer for that particular system. You might want to set the default printer at the user level so that, on a particular system, users can specify their own default printer. If users don't provide a printer name when sending a print job, the print command searches for the default printer in the following order:

| Order | Item |
|---|---|
| First | LPDEST variable |
| Second | PRINTER variable |
| Third | System's default printer |

These variables can be set in the user's .profile file.

## Modifying the Printer with Admintool

The Solaris Admintool can be used to modify a printer after it was added to the system. Modifications that can be made to a printer via the Admintool include:

- Give the printer description.
- Indicate the printer port.
- List file contents.
- Provide fault notification.
- Select default printer.
- Print a banner.
- Accept and process print requests.
- Provide user access list.

To modify a printer via the Admintool, select Edit, Modify from the Printers window shown in Figure 9-7.

### Figure 9-7

The Printers window.

![](img/85737305a4c9aeecbcadd9986d604c02_185_0.png)

After you select Modify from the drop-down menu, the Modify Printer window appears, as shown in Figure 9-8.

### Figure 9-8

The Modify Printer window.

![](img/85737305a4c9aeecbcadd9986d604c02_185_1.png)

Modify the selected printer by selecting or filling in the appropriate fields in the Modify Printer window.

A majority of the system problems I respond to are printer related. This chapter introduced you to the Solaris print system and the lpsched daemon. Chapter 10, “Process Control,” will explore all of the Solaris processes; for a more detailed discussion of the lpsched daemon, refer to the Solaris System Administrator’s Guide.

## CHAPTER

## 10

## Process Control

The following are the test objectives for this chapter:

- Describe a UNIX process
- Understand how to send a signal to a UNIX process
- Understand how UNIX schedules processes
- Understand how to use the UNIX batch-processing facilities

![](img/85737305a4c9aeecbcadd9986d604c02_187_0.png)

Solaris is a multitasking environment in which a number of programs run at the same time. Each Solaris program is called a process. A process is a single program running in its own address space. A process under Solaris consists of an address space and a set of data structures in the kernel to keep track of that process. The address space is a section of memory that contains the code to execute a task. The kernel must keep track of the following data for each process on the system:

- Address space
- Current status of the process
- Execution priority of the process
- Resource usage of the process
- Current signal mask
- Ownership of the process

## Viewing a Process

A process is distinct from a job or command which may be composed of many processes working together to perform a specific task. Each process has a process ID associated with it and is referred to as a pid. You can look at processes that are currently executing by using the ps command. A process has certain attributes that directly affect execution. They are listed in Table 10–1.

Table 10-1 Process Attributes

| Attribute | Description |
|---|---|
| PID | The process identification, a unique number that defines the process within the kernel |
| PPID | The parent PID (the creator of the process) |
| UID | The user ID number of the user who owns this process |
| EUID | The effective user ID of the process |
| GID | The group ID of the user who owns this process |
| EGID | The effective group ID that owns this process |
| Priority | The priority at which this process runs |

Use the ps command to view processes currently running on the system. Adding the -l option to the ps command displays a variety of other information about the processes currently running, including the state of each process (listed under S). The codes used to show the various process states are shown in Table 10–2.
