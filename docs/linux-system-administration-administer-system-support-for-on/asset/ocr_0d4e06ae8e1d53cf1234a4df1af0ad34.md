![](bbox=[0.14, 0.11, 0.26, 0.18])

> For more details on how to setup a printcap file, please see the Printing-HOWTO on the CD-ROM.

Once you have your printer setup, you have several commands that will help you control your printers and allow the users to access them. One of the most useful tools that you have is the `lpc` command, which is the line printer control command.

```
``` 
tigerden:/home/stripes~ lpc 
lpc> 
```
```

Once you type `lpc` on the command line, your prompt will change. This will put you in the control prompt for the printer. As root, you can disable or enable a printer, disable or enable a printer's queue, rearrange the priority of jobs in a spooling queue, or view the printer's status.

```
``` 
lpc> help 
Commands may be abbreviated. Commands are:
abort    enable   disable  help      restart status  topq    ?
clean    exit     down     quit      start   stop    up
```
```

For example, the `status` command output may look something like this:

```
``` 
lpc> status 
lpc:
        queuing is enabled
        printing is enabled
        18 entries in spool area
        printer idle
```
```

This shows you that the printer is accepting jobs, acknowledges that it's printing them, and tells you how many entries are in the queue, as well as what the printer is currently doing. This information may change as jobs get sent to the queue and whether or not the printer is printing. You can also use the `lpc` command from the command line, as in the following example:

```
``` 
tigerden:/home/stripes~ lpc disable all
```
```

This would disable all the printers.

Once you're familiar with the administrative control of a printer with `lpc`, you'll want to be familiar with basic printing commands—like printing a file, viewing the queue, and removing print jobs from the queue. To print a file, use the `lpr` command.