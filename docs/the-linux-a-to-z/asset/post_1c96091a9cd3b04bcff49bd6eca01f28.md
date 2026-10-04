
- `/dev/ttyS0`
- `/dev/ttyS1`
- `/dev/ttyS2`
- `/dev/ttyS3`

As in the case of a modem, a common practice is to create a symbolic link to the serial device from /dev/mouse with a command like:

```
# ln -s /dev/ttyS1 /dev/mouse
```

### 9.3.2 Bus

If you are going out to buy a mouse, then unless you have a good reason to do otherwise, buy a serial mouse. If your computer already has a PS/2 mouse interface, or if you already have a bus mouse, or if you are determined that you want to buy a bus mouse anyway, then that is okay but the installation and configuration of these devices just takes more effort.

In general, a bus mouse will require its own interface card to be fitted inside your computer and the mouse itself will plug into that card. Sometimes a bus mouse interface will be fitted to some other card such as a video adaptor, so that the mouse will not take up an extra slot on your motherboard.

Having fitted the hardware to the machine, you will need to set the interface card up so that it generates an interrupt (IRQ) which does not conflict with any other hardware in your machine and then recompile the kernel to include the appropriate bus mouse support.

By default, most bus mouse interface cards use IRQ 5 as their interrupt number, but lots of other cards also use this as their default, so you will need to take some care over getting the choices right. The IRQ numbers you cannot use are:

```
0 1 2 6 8 13 14 and 15
```

as these are already in use for standard devices and cannot be changed. This leaves you with the choice of:

```
3 4 5 7 9 10 11 and 12
```

Of these, the first four are allocated for use by the standard serial and parallel ports, as follows:

| IRQ | Allocation |
|---|---|
| 3 | COM2 |
| 4 | COM1 |
| 5 | LPT2 |
| 7 | LPT1 |

Many machines have two serial ports and one parallel port fitted, which only leaves the LPT2 port's IRQ as spare. The other IRQs (9 to 12), while spare, cannot be accessed by 8-bit ISA cards, which includes most of the stand alone bus mouse interface cards. So you could have some problems.

### 9.3.3 gpm

One particularly useful application that is available under Linux is gpm. This command actually runs as a daemon, and would usually be executed at system boot time from within one of the standard rc.XXX files (usually rc.local).

What this daemon does is to allow you to use cut and paste facilities on a virtual terminal screen or between virtual terminals. With gpm running, moving the mouse will cause a mouse cursor to appear which moves in step with the mouse. Move the mouse cursor to the start of the block of text you wish to cut. Then press the left mouse button, move the mouse to the end of the text block and release the mouse button again. This should have marked the block of text on the screen. Now pressing the center button on a three-button mouse, or the right button on a two-button mouse will paste the marked text in at the current text cursor position. It is also possible to change virtual consoles after marking a block of text so that the block can be pasted into a different application.

When you run the gpm command you need to specify the type of mouse you have fitted to your machine with a command like the following:

```
# gpm -t msc &
```

where the list of mouse types supported by gpm includes:

- ms microsoft serial mouse;
- msc mouse systems serial mouse;
- bm busmouse protocol bus mouse;
- ps2 PS/2 bus mouse.

## 9.4 Printers

Most PC printers use a parallel port as a Centronics interface. In a DOS environment the printer ports are called LPT1 and LPT2. The equivalent device special files under Linux are:

/dev/lp1
/dev/lp2

Most systems will only have one printer installed, usually as /dev/lp1.

If you are used to using a printer in a DOS environment then you will be used to having direct and sole access to it. Remember, however, that Linux is a multi-user and multi-tasking operating system so that even though, in your particular case, you may be the only user, provision still needs to be made to operate a printer in an environment where several users may be making simultaneous requests to print.

The standard way to solve this problem is to use a print spooling program. With a print spooler in operation any print requests that are made are not routed directly to the printer but are sent to files in a spool directory instead. Then, a separate program can pick up the print jobs one at a time from the spool directory and send them to the printer.

Under Linux, the situation is slightly more complex than this simple scenario suggests. This is because, as well as printing to a local printer, it is also possible to print on remote printers over a network.

### 9.4.1 Print Services

The task of scanning the spool directories (there is one directory for each printer) and printing any waiting files is performed by a program called lpd. The lpd program is actually the line printer daemon which needs to be executed at system boot time, usually from within the startup file rc.M or rc.inet2.

The four standard commands to submit, remove, monitor and control print jobs are:

- **lpr** This is the command that allows you to submit a print job. Essentially, this means that your document will be copied to the spool directory for the printer, ready for lpd to pick up and print.
- **lpq** When it is submitted, each print job is given a unique job number. The lpq command will give a list of all the jobs in the spool directory for a particular printer along with the job number for each job on the list.
- **lprm** Once you know the job number for a particular print job (given by lpq) you can use the lprm command to remove it from the spool directory so it won’t be printed. If you specify ‘-’ instead of a job number it will remove all the print jobs belonging to you.
- **lpc** This is the print system control program. It makes several different status and control commands available. However, as an ordinary user you can only use it to display the status of printers, spool queues, and daemons. All the other lpc commands which allow you to start and stop printers, spooling and print daemons, require you to be logged in as root.

By default, all these commands operate on the printer called lp. If you want to specify an alternative printer you can use the -Pname command line switch, where name is the name of the printer to use. Or, you can set the PRINTER shell variable up with the printer name instead.

### 9.4.2 printcap

All that needs to be done now, is to see how the various print service configuration options are set up. This is all done in the file:

/etc/printcap

This file is just a text file so you can use vi to modify it (if you login as root). The contents of the file are called printcap entries. Each printcap entry is just a set of configuration options – one printcap entry for each printer to which you will have access.

Two typical printcap entries are shown next, the first is for output to a local dumb dot matrix printer called lp. The second is for access to an HP 4L laser printer called hp, available over the network on a machine called gregory:

```
lp|starsg10:\n:lp=/dev/lp1:\n:sd=/usr/spool/lp:\n:lf=/usr/spool/lp/err-log:\n:mx#0:\n:sh:
```

```
hp|hp41:\n:lp=:\n:rm=gregory:\n:sd=/usr/spool/hp:\n:lf=/usr/spool/hp/err-log:\n:if=/usr/local/bin/apsfilter:\n:mx#0:
```

The first thing to notice is that printcap entries must only occupy a single logical line, with '\' characters used to signify that the line is not yet complete.

The first field of each printcap entry starts at the beginning of a line and contains a list of names by which the printer may be known. The individual names are separated by '|' characters.

After the first field in each entry there follows a set of options and, where appropriate, their values.

Let us now work through the two printcap entries in turn, lp entry first. After the name field, the second line specifies the device special file to which the printer is attached (/dev/lp1 here). The third line specifies the spool directory for this printer as /usr/spool/lp. The fourth line gives the path to a log file which will be used to record any error messages generated while printing. The mx option specifies the maximum file size (in 1Kb blocks) that can be printed. A value of zero (as here) indicates that the size is unrestricted. The final option in this entry (sh) takes no parameters and just specifies that header page printing should be suppressed.
