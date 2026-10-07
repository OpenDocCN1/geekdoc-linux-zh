Note The output format of LPRng, as shown above, differs from the format of the original lpd's lpq. LPRng's listing is more complete, but lpd's provides much of the same critical information, including a job ID number and the name of the file being printed.

# lpc

The LPRng System Control program, or *lpc*, provides the capability to disable or enable a print queue, to reorder the print jobs in a queue, and to obtain status information about a printer, a queue, or a job. These commands are applicable to any printer in the */etc/printcap* file as specified by the associated name or to all printers.

If issued without an argument, the *lpc* session will be interactive and an *lpc>* prompt will be returned. You can also include the *lpc* command in a script, using the following format:

```
lpc [subcommand]
```

The available subcommands are as follows:

+   *   **abort** Terminates any printing in progress and then disables further printing to the specified printer(s). The queue is left intact so that the waiting print jobs will be printed when the *start* command is next issued. Sometimes, if a printer has stopped printing for no apparent reason, issuing the *abort* command followed by the *start* command will get things going again.
*   **disable** Turns the queue off so that it won't accept any more jobs, although the superuser can still queue print jobs. Printing is not halted, so anything in the queue already or added by the superuser will print. When a printer is to be deactivated, you should issue the *disable* command followed by the *stop* command.
*   **down** Turns the specified print queue off, disables printing to that queue, and logs a message to the printer status file. Subsequent attempts to run the *lpc* command will indicate that it is down and output the status message.
*   **enable** Enables spooling on the specified printer's queue so that it will accept new jobs.
*   **exit** Terminates the interactive *lpc* session.
*   **reread** Tells the *lpd* daemon to reread its configuration file.
*   **start** Enables printing and starts a spooling daemon for the specified printer(s).
*   **stop** Stops *lpd* after the current job has been completed and disables printing.
*   **topq [printer] [jobs]** Places the jobs in order at the top of the queue (after the currently printing job) for the specified printer(s). Unless *topq* has been used to reorder them, the jobs will be in FIFO order (first in first out).
*   **up** Enables the queue for the specified printer and starts a new printer daemon for that queue.

As an example, suppose you want to reorder the jobs in the *lexmark* print queue so that job 186 from the earlier *lpq* example prints before job 182. (Ordinarily, job numbers are assigned in ascending order according to print order.) You might use the following command to accomplish this