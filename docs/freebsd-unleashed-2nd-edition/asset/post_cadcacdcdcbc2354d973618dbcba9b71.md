
## 选项表

| Option | Description |
| :--- | :--- |
| -S | Uses symbolic links. Rather than copying the file to the spool directory, this option will simply create a symbolic link to the spool directory from the existing file. This allows files too large to fit in the spool area to be printed. If you use this option, be careful that you do not modify or delete the file before it has finished printing. |
| -#n | Here, n is the number of copies of each file that should be printed. (This feature can be disabled.) |
| -J job | Here, job is the name of the job that should be printed on the banner page. By default, it will be the name of the first file that is specified. |
| -T | Specifies the title name that pr should use on the header at the top of the page. By default, this will be the filename. This option only applies if the -p option has also been used. |
| -i n | Here, n represents the number of columns that the printed output will be indented by. |
| -w n | Here, n represents the page width in columns. This only applies if the -p option has also been used. |

## Printing from X-Windows

Different X-Windows applications will have different means of printing, but here is an example from Netscape if you want to print a Web page, for instance.

To print a file from Netscape, select File and then choose Print from the menu. The Print dialog box is shown in Figure 15.1.

![](img/48eec858cce7dfb89da36a4d40b7daf3_383_0.png)

FIGURE 15.1 The Print dialog box in Netscape. Notice that if you click the File button at the top, the filename will be netscape.ps. Netscape outputs PostScript data when it prints.

In the “Print To:” section at the top, you can select whether you want to send the output to a printer or to a file. If you select Printer, the Print Command box becomes active and you can type in your command. Notice that it defaults to 1pr, which is the same program you used to print from the command line. If you want, you can supply additional options to 1pr here, such as having it e-mail you when it is done or print more than one copy. (See the section on 1pr earlier in this chapter for details.)

Most X-Windows programs can also output to a file. When they do, they will usually create a PostScript file that can then be sent to a PostScript printer directly or run through GhostScript and sent to a non-PostScript printer.

Like many other Unix programs, Netscape has no printer drivers. It simply outputs in PostScript. This demonstrates the need for GhostScript if you are not running a printer that understands PostScript.

### Printing in StarOffice

If you have StarOffice installed, you can configure its printer by double-clicking the Printer Setup icon on the desktop. You will get a dialog box like that shown in Figure 15.2.

![](img/48eec858cce7dfb89da36a4d40b7daf3_384_0.png)

FIGURE 15.2 The Printer Configuration dialog box in StarOffice. Notice that StarOffice has printer drivers included (bottom box) for many different printer models.

Because StarOffice comes with a large selection of drivers for various printers, it eliminates the need for using GhostScript to translate PostScript. You can simply select your printer model from the list and click Add New Printer, and it will be installed as the default printer. You can then use the Configuration button and such to configure the printer.

If you do not install a printer, StarOffice uses the default “Generic Printer in queue,” which sends PostScript output to `lpr`.

> **TIP**
> Even if you do have GhostScript installed, you will probably want to use one of the native drivers in StarOffice because it may have better support for the various features of your printer that can be accessed directly from StarOffice, without you having to modify GhostScript filter options.

## Using the `lpq` Command to Check the Status of Print Jobs

The `lpq` command can be used to check the status of jobs that are waiting in the print queue. If it is called without any arguments, `lpq` will report the status of all jobs currently in the queue for the default printer. The default printer is checked in the following order: If the `PRINTER` environment variable is set, that printer is considered to be the default printer. If the `PRINTER` environment variable is not set, the printer that is aliased to `lp` in `/etc/printcap` will be used as the default.

`lpq` can also be called with a job number to show only the status of a particular job or with a username to show only the status of jobs owned by a particular user. The output of `lpq` will look something like this:

```bash
bash$ lpq -P simba
simba is ready and printing

Rank  Owner  Job   Files                         Total Size
active  mike   5    /home/murban/sample.txt       2000 bytes
2nd    mike   6    /home/murban/sample1.txt       2500 bytes
3rd    jack   7    /home/jack/myfile.txt          3200 bytes
4th    jack   8    ...                             5500 bytes
```

The `-P` option tells `lpq` to report on a printer other than the default—in this case, the printer named `simba`. All of the options to `lpq` will be explained later.

The information given by `lpq` is pretty self-explanatory.

The first line tells you the printer is currently doing. In this case, the printer is ready and printing. If the printer is stalled, out of paper, jammed, and so on, you may see other things listed here instead.

The example here shows four jobs in the queue; one is active, and the others are ranked as to when they will be printed. A few other things are worth pointing out. The third column, labeled Job, shows the job ID number assigned to a particular job. If you need to cancel a print job (explained later), you will need this job ID number. Also, the fourth column lists the file or files that are being printed. Notice that the fourth job in this example is listed as just three dots. This means that the pathname of the file is too long to fit in the list, so lpq simply didn't list it.

The `lpq` command has a few other options, as shown in Table 15.5.

**TABLE 15.5 Options to lpq**

| Option | Description |
| :--- | :--- |
| -P name | Here, `name` is the name of a printer. This will cause `lpq` to show information on a printer other than the default one. |
| -l | This option will cause information about each one of the files in the queue to be displayed, even if the information causes the display to break across a line. (In the previous example, this command would cause the filename to show; it currently shows up as three dots because it is too long to fit.) |
| -a | Causes `lpq` to display the status of all local queues for all printers. |

### Removing Jobs from the Queue with the lprm Command

The `lprm` command can be used to remove print jobs that are currently in the queue and sometimes to remove print jobs that are currently printing. If `lprm` is run without any command-line arguments, it will remove whatever job is currently printing on the default printer if that job belongs to the user running `lprm`. If the currently running job does not belong to the user running `lprm`, the command will have no effect. If the root user runs `lprm` with no options, the command will remove the currently printing job from the default printer, no matter who the job belongs to.

Running `lprm` with a job number as an argument will remove the job with that ID number from the queue of the default printer, assuming that you own the job and that you are not the root user. Normal users can only remove jobs that belong to them. The root user can remove any job. Here is an example:

```bash
bash$ lprm 5
dfA001simba.sampling.org dequeued
cfA001simba.sampling.org dequeued
bash $
```

The first file that is dequeued in this example is the data file for the job. This is basically a copy of the file in the printer's spool directory. The second file that is dequeued is a control file.

Note that the system may take some time to respond when you run `lprm` (up to several seconds). It may seem that `lprm` has hung. Don't worry; it hasn't. Wait a few seconds, and you should get your prompt back.

If you try to delete a job that does not belong to you, and you are not the root user, `lprm` will respond with the message `Permission denied`.
