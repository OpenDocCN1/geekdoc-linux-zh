
CUPS class is a group of printers to which a user can submit a print job. Whichever printer within the class is first available is used to print the job.

For example, suppose you manage the printing for a busy office that has three high-capacity laser printers that you have defined as lexmark1, lexmark2, and lexmark3. Without classes, users would try to guess which printer to send their print job to so it wouldn’t have to wait for another long job to finish; polite users might send out a department-wide e-mail: “380 page job going to lexmark2.” You decide to use CUPS and create a class called lexmarks that includes all three lexmark print queues. Now users send all print jobs to lexmarks. Each time any one of the three printers finishes a print job, CUPS sends the next print job to that printer. Users get the fastest possible service. In exchange, they have to check three different printers to see which one their print job came out on. (Printers within a class are typically located next to each other in an office.)

To create a class in CUPS, click the Classes button at the top of the CUPS page and then click the Add Class button on the Classes page. The page that appears lets you define a name, location, and description. You must include at least a name, such as “lexmarks.” In a large department with many users or printers, it’s also a good idea to enter a location and description, for example “Downstairs by Robin’s Cube” and “Main dept. laser printers.”

When you choose Continue, you see a listing of all printers defined within CUPS. You select all of the printers that should be included in the class you are defining. Then choose Continue. A confirmation page shows you that the class was successfully completed. If you return to the Classes page by clicking Classes at the top of the page, you see that your class is shown with most of the same options as a regular printer, except that the icon shows multiple printers, and many of the buttons differ. Figure 12-16 shows the Classes page.

![](img/43f64015de86d989e30eff5bb284fb96_578_0.png)

Figure 12-16 The Classes page within the CUPS configuration

Users can still send print jobs to an individual printer that is part of a class (such as lexmark2 in the previous example). But the class provides a more efficient method of distributing print jobs on a busy network with many users and more than one printer.

## Managing Printing

You learned in Chapter 3 how to submit a print job from the command line. Printing from a graphical application is even easier: you typically select Print from the File menu and choose Print in the dialog box that appears.

Though submitting print jobs is easy, as a system administrator you are likely to spend a lot of time managing printing. Printers have many moving parts and are more subject to breakdowns than anything inside a computer. Printing also consumes resources such as paper and toner that must be replenished even when the system is working correctly. (Some companies have an employee designated to take care of these things who does not manage other aspects of printing.) For all of these reasons, many organizations establish a printing policy: a brief statement of rules describing how printing resources can be used and how printers should be managed.

Linux includes several utilities to help you manage printing resources. One of these is the lpc utility. This command-line utility lets you control LPRng or CUPS printing, specifying how print jobs are accepted and processed.

> Many Linux system administrators prefer to use one of the graphical utilities described later in this section instead of lpc.

Though it was not obvious in Chapter 3, Red Hat Linux and Fedora use an alternatives printing system that maps the command you enter to different programs based on which printing system you are using: LPRng or CUPS. You can view and configure this system using the alternatives command. The actual symbolic links are maintained in the directory /etc/alternatives. Both the lpr command and the lpc command are actually symbolic links. The lpc command, for example, is a link to /etc/alternatives/print-lpc, which in turn points to the appropriate control program for the LPR or CUPS printing system. In Fedora Core 2, the default control program referred to by this link is /usr/sbin/lpc.cups. The link is changed if you switch to the LPRng printing system, which would be unusual in Fedora because the newer CUPS system is the default. The control programs for both LPR and CUPS provide similar functionality, but act on different underlying systems.

Using lpc you can:
- Prevent new print jobs from being accepted by a print queue.
- Prevent print jobs from being sent to a printer.
- Cancel a print job that is currently being printed.

See the status of any printer (such as whether it is enabled, whether the corresponding print queue contains any print jobs, or how much of the current document has been sent to the printer).

You must be logged in as the root user to use lpc. You can include an lpc command as a parameter on the command line. This command displays the status of the default printer:

```
# lpc status
```

You can also use lpc interactively to enter multiple commands. To begin using lpc in interactive mode, enter the utility name without any parameters:

```
# lpc
lpc>
```

Table 12-1 lists the commands that you can use at the lpc prompt or as parameters to the lpc command (if you prefer not to use the interactive mode for some tasks).

For each of the commands shown, lpc acts on the default printer (the first one listed in the printcap file) unless you specify a printer name. For example, if the first printer in printcap is hp, using this command brings down the hp printer:

```
# lpc down
```

If the printcap file contains a definition of another printer named stylus, you can use this command to bring down the stylus printer:

```
# lpc down stylus
```

## Table 12-1 lpc Commands

| Command | Description | Example (noninteractive mode) |
|---|---|---|
| help | Display a list of all lpc commands | lpc help |
| status | Display status of the lpd printer daemon and the print queue indicated (or the default if none is indicated) | lpc status |
| abort | Cancel the print job currently being printed (use the start command to restart printing) | lpc abort |
| stop | Stop sending print jobs to the printer after the current print job has finished printing | lpc stop |
| start | Start sending print jobs to the printer (used after abort or stop) | lpc start |
| disable | Prevent users from submitting new print jobs | lpc disable |
| enable | Allow users to submit new print jobs | lpc enable |
| down | Stop sending print jobs to the printer and prevent new print jobs from being submitted (equivalent to using stop and disable) | lpc down |
| up | Begin sending print jobs to the printer and allow new print jobs to be submitted (equivalent to using start and enable) | lpc up |

## Table 12-1 lpc Commands (continued)

| Command | Description | Example (noninteractive mode) |
|---|---|---|
| exit or quit | Exit the lpc program | Used only in interactive mode |
| restart | Attempt to restart the lpd printer daemon (equivalent to using the command /etc/rc.d/init.d/lpd restart) | lpc restart |
| clean | Remove any temporary, data, or control files that could not be printed | lpc clean |
| topq | Move a print job to the top of the named print queue; this command requires a printer name (where the print job is placed) and the print job number (which you can obtain using the lpq command) | lpc topq hpj 16 |

When using any of the lpc commands (except topq), you can use all to refer to all printers. For example, to completely shut down printing, so that no print jobs can be submitted and all printing stops after the current print jobs are finished, use this command:

```
# lpc down all
```

> NOTE The lpr command you learned previously uses a -P parameter to define the printer name. For the lpc command you simply add the printer name as an additional parameter.

Figure 12-17 illustrates how some key lpc commands affect the printing process. The same terms you see in the figure are used in the lpc man page and in graphical print management tools.

![](img/43f64015de86d989e30eff5bb284fb96_581_0.png)

## Figure 12-17 Using lpc to control the printing process
