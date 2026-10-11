
After a print job is in the print queue, it is ready to be printed. If the printer is **enabled**, and ready to accept the print job, the cups daemon then sends the print job from the print queue to the printer and removes the copy of the print job in the print queue. Conversely, if the printer is **disabled**, the print job remains in the print queue.

![](img/09bf13b782f71165e17bb3839040c96a_428_0.png)

### NOTE
Sending print jobs from a print queue to a printer is commonly called **printing**.

An example of this process for a printer called printer1 is illustrated in Figure 11-1.

![](img/09bf13b782f71165e17bb3839040c96a_428_1.png)

### **FIGURE 11-1** *The print process*

To see a list of all printers on the system and their status, you can use the -t (total) option to the **lpstat command**, as shown in the following output:

```bash
[root@server1 root]# lpstat -t
scheduler is running
system default destination: printer1
device for p1: parallel:/dev/lp0
p1 accepting requests since Jan 01 00:00
printer p1 is idle. enabled since Jan 01 00:00
[root@server1 root]# 
```

The preceding output indicates that there is only one printer on the system called *printer1* that prints to a printer connected to the first parallel port on the computer (//dev/lp0) and that there are no print jobs in its print queue. In addition, the cups daemon (*scheduler*) is running and accepting jobs into the print queue for this printer. Also, the cups daemon sends print jobs from the print queue to the printer because the printer is enabled.

# Chapter 11 COMMON ADMINISTRATIVE TASKS

You can manipulate the status of a printer using either the accept, reject, enable, or disable commands followed by the printer name. Thus, to enable spooling and disable printing for the printer printer1, you can use the following commands:

```bash
[root@server1 root]# accept printer1
[root@server1 root]# disable printer1
[root@server1 root]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Jan 01 00:00
printer printer1 disabled since Jan 01 00:00 - Paused
[root@server1 root]# 
```

Any print jobs now sent to the printer printer1 are sent to the print queue, but remain in the print queue until the printer is started again.

> **NOTE**
> If you want to enable a printer, you must specify the full path to the enable command (/usr/bin/enable) because there is also a BASH shell function called enable.

You can also use the -r option to the disable and reject commands to specify a reason for the action, as shown in the following output:

```bash
[root@server1 root]# disable -r "Changing toner cartridge" printer1
[root@server1 root]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Jan 01 00:00
printer printer1 disabled since Jan 01 00:00 - Changing toner cartridge
[root@server1 root]# 
```

## Managing Print Jobs

Recall that you create a print job by using the lp command. To print a copy of the /etc/inittab file to the printer printer1 shown in earlier examples, you can use the following command, which returns a print job ID that you can use to manipulate the print job afterward:

```bash
[root@server1 root]# lp -d printer1 /etc/inittab
request id is printer1-1 (1 file(s))
[root@server1 root]# 
```

## PRINTER ADMINISTRATION

The lp command uses the -d option to specify the destination printer name. If this option is omitted, the lp command assumes the default printer on the system. Because printer1 is the only printer on the system and, hence, is the default printer, the command lp /etc/inittab is equivalent to the one used in the preceding output.

![](img/09bf13b782f71165e17bb3839040c96a_430_0.png)

### **NOTE**

> You can set the default printer for all users on your system by using the lpoptions -d printername command, where printername is the name of the default printer. This information is stored in the /etc/cups/lpoptions file.
>
> Each user on a Linux system can specify his own default printer by adding the line default printername to the .lpoptions file in his home directory, where printername is the name of the default printer. Alternatively, you can use the PRINTER or LPDEST variables to set the default printer. For example, to specify printer2 as the default printer, you can add either the line export PRINTER=printer2 or the line export LPDEST=printer2 to an environment file in your home directory such as .bash_profile.

Table 11-1 lists some common options to the lp command.

**Table 11-1 Common options to the lp command**

| Option | Description |
|---|---|
| -d *printername* | Specifies the name of printer to send the print job. |
| -i *print job ID* | Specifies a certain print job ID to modify. |
| -n *number* | Prints a certain *number* of copies. |
| -m | Mails you confirmation of print job completion. |
| -o *option* | Specifies certain printing options. Common printing options include the following:<br>*cpi = number*—Sets the characters per inch to *number*<br>*landscape*—Prints in landscape orientation<br>*number-up = number*—Prints *number* pages on a single page, where *number* is 1, 2, or 4<br>*sides = string*—Sets double-sided printing, where *string* is either ‘two-sided-short-edge’ or ‘two-sided-long-edge’ |
| -q *priority* | Specifies a print job priority from 1 (low priority) to 100 (high priority). By default, all print jobs have a priority of 50. |

You can also specify several files to be printed using a single `lp` command by specifying the files as arguments. In this case, only one print job is created to print all of the files. To print the files `/etc/hosts` and `/etc/issue` to the printer *printer1*, you can execute the following command:

```bash
[root@server1 root]# lp -d printer1 /etc/hosts /etc/issue
request id is printer1-2 (2 file(s))
[root@server1 root]# 
```

The `lp` command accepts information from Standard Input; thus, you can place the `lp` command at the end of a pipe to print information. To print a list of logged-in users, you can use the following pipe:

```bash
[root@server1 root]# who | lp -d printer1
request id is printer1-3 (1 file(s))
[root@server1 root]# 
```

To see a list of print jobs in the queue for *printer1*, you can use the `lpstat` command. Without arguments, this command displays all jobs in the print queue that you have printed:

```bash
[root@server1 root]# lpstat
printer1-1        root            2048  Fri 29 Jul 2005 06:18:22 PM EDT
printer1-2        root            3072  Fri 29 Jul 2005 07:05:49 PM EDT
printer1-3        root            1024  Fri 29 Jul 2005 07:06:50 PM EDT
[root@server1 root]# 
```

Table 11-2 lists other options that you can use with the `lpstat` command.

**Table 11-2 Common options to the lpstat command**

| Option | Description |
| :--- | :--- |
| -a | Displays a list of printers that are accepting print jobs |
| -d | Displays the default destination printer |
| -o *printername* | Displays the print jobs in the print queue for *printername* only |
| -P | Displays a list of printers that are enabled |
| -r | Shows whether the cups daemon (scheduler) is running |
| -t | Shows all information about printers and their print jobs |

To remove a print job that is in the print queue, you can use the **cancel command** followed by the print job IDs of the jobs to remove. To remove the print job IDs printer1-1 and printer1-2 created earlier, you can use the following command:

```bash
[root@server1 root]# cancel p1 p1-1 p1-2
[root@server1 root]# lpstat
      printer1-3          root          3072     Fri 30 Jul 2005 07:05:49 PM EDT
[root@server1 root]# 
```

You can instead remove all jobs started by a certain user; simply specify the -u option to the cancel command followed by the user name. To remove all jobs in a print queue, you can use the -a option to the cancel command, as shown in the following example:

```bash
[root@server1 root]# cancel -a
[root@server1 root]# lpstat
[root@server1 root]# 
```

Not all users might be allowed access to a certain printer. As a result, you can restrict who can print to certain printers by using the lpdadmin command. For example, to deny all users other than root and user1 from printing to the printer1 printer created earlier, you can use the following command:

```bash
[root@server1 root]# lpdadmin -u allow:root,user1 -u deny:all -d printer1
[root@server1 root]# 
```

## The LPD Printing System

Although CUPS is the preferred printing system for Linux computers today, many older Linux computers use the traditional Line Printer Daemon (LPD) printing system. In this printing system, the lpr command is used to print documents to the print queue much like the lp command, the lpc command can be used to view the status of printers, the lpq command can be used to view print jobs in the print queue much like the lpstat command, and the lprm command can be used to remove print jobs much like the cancel command.

For those users who are used to using the LPD printing system, CUPS contains versions of the lpr, lpc, lpq, and cancel commands. The following output displays the status of all printers on the system, prints two copies of /etc/inittab to printer1, views the print job in the queue, and removes the print job:

```bash
[root@server1 root]# lpc status
printer1:
      printer is on device 'parallel' speed -1
      queuing is enabled
      printing is enabled
      no entries
      daemon present
[root@server1 root]# lpr -#2 -P printer1 /etc/inittab
[root@server1 root]# lpq
printer1 is ready and printing
      Rank Owner Job File(s) Total Size
      active root 1 inittab 2048 bytes
```
