
## FIGURE 10.7
*The Admintool’s Add Access to Printer dialog box*

![](img/256e02a6afce528d264a8d911fa0ff20_436_0.png)

Follow these steps to add a new attached printer to a print server:

1. Start the Solaris Print Manager (see “Adding Printer Access”).
2. Select the New Attached Printer command from the Printer menu. The New Attached Printer dialog box appears.
3. Enter the printer name and select the printer port, printer type, file contents, and fault notification options. Set the Default Printer and Always Print Banner options.
4. In the User Access List list box, enter the name of users or groups or enter **all** for all users.
5. Click the Apply button to continue adding additional attached printers. Or click the OK button to return to the main Print Manager window.

You will see the attached printer added to the Print Manager, and the printer’s information will be added to the appropriate configuration files.

Finally, test that the network printer was correctly attached by using the `lp -d <printname> <filename>` command to print a test file.

You can enter the following sequence of commands at the command line to attach a printer and set its attributes for a print server:

```bash
# chown lp /dev/term/b
# chmod 600 /dev/term/b
# lpadmin -p flash -v /dev/term/b
# lpadmin -p flash -T PS
# lpadmin -p flash -I postscript
# cd /etc/lp/pd
# for <filter> in *fd;do
> name=basename $<filter> .fd'
> lpfilter -f $name -F $<filter>
# accept flash
destination 'flash' now accepting requests
# enable flash
printer 'flash' now enabled
# lpadmin -p flash -D 'First floor laser'
# lpstat -p flash
printer flash is idle. enabled since Dec 20 10:50 2001.
available.
```

In the preceding sequence, the second line gives the LP print service ownership of the port so that no other process can access it. Line 4 sets the printer type, and line 5 sets the file contents type (PS). Lines 7 through 9 set the print filters for the print server. The -D option sets the description, and the last two lines (starting with lpstat) show that the printer is ready to print.

Finally, you can use a very similar process to add a new network printer to a print server found elsewhere on the network (not attached). In addition to all of the parameters that were required for adding an attached printer to a print server, you will be required to specify a destination and protocol. You do not need to specify a port address for a nonattached network printer serviced by a print server.

To add a new attached printer to a print server, follow these steps:

1. Start the Solaris Print Manager.
2. Select the New Network Printer command from the Printer menu. The New Network Printer dialog box, shown in Figure 10.8, appears.
3. Enter the printer name and a description and select the correct settings for the printer type, file contents, fault notification, destination, and protocol. As before, set the Default Printer and Always Print Banner behaviors using the corresponding check boxes.
4. In the User Access List list box, enter the name of users or groups, or enter all for all users.
5. Click the Apply button to continue adding additional network printers. Or click the OK button to return to the main Print Manager window.

You will see the network printer added to the Print Manager, and the printer's information will be added to the appropriate configuration files.

![](img/256e02a6afce528d264a8d911fa0ff20_438_0.png)

## FIGURE 10.8
The New Network Printer dialog box

### Printing a File

You can use the Default Print control on the CDE front panel to print a file on the Solaris desktop. Just drag and drop a file from one of the File Manager's windows to the Printer control on the front panel.

You use the `lp` command to print from the command line. When you specify a print job with the `lp` command, the job is placed into the LP print service into the print queue for the printer specified, the request ID number is returned, and the shell prompt is refreshed. When you don't specify a printer, the `lp` command uses the default printer. The command in that case is simply entered as `lp <Filename>`. When a print job completes, Solaris sends an e-mail to the user who generated the print request.

When you want to specify a printer other than the default printer, use the following command:

```bash
$ lp -d flash /<mydirectory>/<myfile name>
```

Solaris returns output similar to the following:

```text
Request id is flash-7 (1 file)
$
```

Should you print to a printer that is not available on your system, Solaris posts the following error message:

```text
$ lp -d spot /<mydirectory>/<myfilename>
UX:lp: ERROR: Destination `spot' is unknown to the LP print
service
$
```

The `lp` command takes the following options:

- **-c option**: The `-c` (copy) option copies a file as output to the location you specify and before your print request is printed.
- **-d option**: The `-d` option specifies the destination printer's name.
- **-h option**: The `-h` (header) option adds a header that you specify to the top of each page in your print output.
- **-n option**: Use the `-n` (number) option to specify the number of copies of the print job to print.
- **-o option**: The `-o` (no banner) option suppresses the printing of a banner page with your print job.
- **-t option**: The `-t` (title) option is used to print a title of the print job on the banner page. A banner page is a page printed prior to the print job that separates the print job from other jobs in the printer's output.
- **-w option**: The `-w` (write) option writes a message to the console of the superuser when the print job has completed printing.

As an example of a compound option, consider the following command that prints three copies and sends you e-mail when the print job completes its execution:

```bash
$ lp -n3 -m /<mydirectory>/<myfilename>
```

When using a SunSoft print client, you can use either the `lp` or `lpr` command to specify a print request. As part of that print request, you need to specify the target printer and the print class in any of the following styles or manner:

- **Atomic style**: The print command takes the form `lp -d <printername> <filename>`.
- **POSIX style**: The print command uses the format `lpr -P <servername> <printername> <filename>`.
- **Context-based style**: Use the format `lpr -d <departmentname>/<servername>/<printername> <filename>`.

The LP print service manages forms printed on a printer and alerts the user when it cannot successfully print a form. You must provide the description of how to print a form, and you must also manually mount the form stock into the target printer, but the LP print service will provide feedback as to the progress of the form’s printing. Users can specify a form print job, but it takes a superuser to mount a specific form in a printer and make it available to other users.

Similar to working with forms, the LP print service can manage print wheels on impact printers such as letter-quality printers that typically use removable printer balls or daisy wheels where the ribbon is impacted by the ball or wheel to create a specific font or character set. The LP print service can detect which character set is in use and will notify the superuser when the character set the user specified isn’t in the printer. The print job remains in the print queue until the correct character set in the impact printer becomes available.

The `cancel` command is used to delete a print request that is in the print queue or to terminate a print job that is currently executing. To cancel a job, you must specify the job ID as part of the command, as shown here:

```bash
$ cancel flash-2 flash-3
request "flash-2" cancelled
request "flash-3" cancelled
```

If you want to cancel the currently printing job, just give the command `cancel <printname>`.

## Summary

The Solaris print subsystem is based on the System V printing subsystem. In this chapter, I showed you how, using the LP print system commands, you can completely set up and administer a printer and specify print jobs. Solaris maintains a print queue for each printer and a scheduler for managing print jobs. Print jobs are spooled and printed on a print server. Print logs are stored on Solaris and can be used to troubleshoot the Solaris print process.

This chapter also included a discussion of the Solaris Print Manager, which offers graphical tools for installing and managing printers, and how to use the AdminTool as a graphical tool for installing and managing printers. Most of the time, you can use graphical tools to add local and network printers, but certain features require command-line modification.

Finally, you learned about the three methods you can use to print files: from within an application using the Print command, by dragging and dropping files onto the Printer control on the front panel, or by using the `lp` command.
