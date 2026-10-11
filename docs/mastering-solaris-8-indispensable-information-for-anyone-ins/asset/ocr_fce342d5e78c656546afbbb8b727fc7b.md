LP print service will provide feedback as to the progress of the form’s printing. Users can specify a form print job, but it takes a superuser to mount a specific form in a printer and make it available to other users.

Similar to working with forms, the LP print service can manage print wheels on impact printers such as letter-quality printers that typically use removable printer balls or daisy wheels where the ribbon is impacted by the ball or wheel to create a specific font or character set. The LP print service can detect which character set is in use and will notify the superuser when the character set the user specified isn’t in the printer. The print job remains in the print queue until the correct character set in the impact printer becomes available.

The cancel command is use to delete a print request that is in the print queue or to terminate a print job that is currently executing. To cancel a job, you must specify the job ID as part of the command, as shown here:

```
```
$ cancel flash-2 flash-3
request "flash-2" cancelled
request "flash-3" cancelled
```

```

If you want to cancel the currently printing job, just give the command cancel <printname>.

# # Summary

The Solaris print subsystem is based on the System V printing subsystem. In this chapter, I showed you how, using the LP print system commands, you can completely set up and administer a printer and specify print jobs. Solaris maintains a print queue for each printer and a scheduler for managing print jobs. Print jobs are spooled and printed on a print server. Print logs are stored on Solaris and can be used to troubleshoot the Solaris print process.

This chapter also included a discussion of the Solaris Print Manager, which offers graphical tools for installing and managing printers, and how to use the AdminTool as a graphical tool for installing and managing printers. Most of the time, you can use graphical tools to add local and network printers, but certain features require command-line modification.

Finally, you learned about the three methods you can use to print files: from within an application using the Print command, by dragging and dropping files onto the Printer control on the front panel, or by using the lp command.