
printer daemon is started, it reads the /etc/printcap file, discussed earlier. Listing 10.1 shows an example of a printcap file.

## Listing 10.1: An Example printcap File

```text
lp|lp0|lexmark: \
    :sd=/var/spool/lpd/lexmark:\
    :mx#0:\
    :sh:\
    :lp=/dev/lp0:\
    :if=/var/spool/lpd/lexmark/filter:
lpl|hp4000:\
    :sd=/var/spool/lpd/hp4000:\
    :mx#0:\
    :sh:\
    :rm=tennessee:\
    :rp=hp4000:\
    :if=/var/spool/lpd/hp400/filter:
lp2|epson:\
    :sd=/var/spool/lpd/epson:\
    :mx#0:\
    :sh:\
    :if=/var/spool/lpd/epson/filter:\
    :af=/var/spool/lpd/epson/acct:\
    :lp=/dev/null:
```

This printcap file example contains the configuration for a directly connected Lexmark Optra 40, a remote HP LaserJet 4000, and a remote SMB/Windows Epson Stylus Color 800. The first line assigns the local printer's name, in this case lp|lp0|lexmark. This is actually a specification for three names, each separated from the others by vertical bars (|). In this case, users can refer to the printer as lp, lp0, or lexmark, with identical results. lp is the default for the first printer on most systems. The next uncommented line sets the spooling directory for the printer to /var/spool/lpd/lexmark. The line beginning with :mx sets the maximum file size in kilobytes; the 0 in our example sets it to unlimited. The next line sets up the printer to suppress the page header, which when present provides information on who ran the print job, to make sorting print jobs easier in a busy printing environment. The next line sets the printer device name to /dev/lp0. This device name is the printer's hardware device file—the file to which LPRng ultimately sends its output. This name may or may not bear any resemblance to the print spool name defined earlier. The line beginning with :if provides the path to the file that contains the filter information for any print types defined for that printer. These options and more are documented in the printcap man page.

The sample printcap file contains stanzas (sections) for two more printers. The lpl|hp4000 entry is for a printer located on a machine with a hostname of tennessee, located on the same network as the local machine. The difference in this stanza is that instead of an lp line, it contains an rm line, which specifies the machine to which the printer is connected; and an rp line specifying the queue name on that machine. This second queue also has its own spool directory.

The lp2|epson entry is for an SMB/Windows 95/NT printer. The standard Red Hat print queue format doesn't place information on SMB print servers in the printcap file; instead, that information is located in the .config file in the spool directory. For an SMB printer, you must include a username and password for the host machine. For security reasons, the username and password on the Windows machine should *not* be the same as that user's account on the Linux machine. We'll discuss printing to a networked Windows printer later in the chapter.

After reading through the printcap file and printing anything left in the queue, the line printer daemon goes into a passive mode, waiting for requests to print files, reorder print jobs in the queue, or display the waiting print jobs. It uses the system calls `listen` and `accept` to determine whether any such requests are made.

As mentioned above, the line printer daemon package includes other programs necessary to the printing functionality. These binaries perform specific functions, which we'll look at next.

## lpr

The `lpr` program is the spooling command that makes requests of `lpd`. `lpr` makes contact with the line printer daemon when it needs to put a new print job into the spool. The format is basic:

```text
lpr path-to-file [arguments]
```

When you print from an application under Linux, the program runs `lpr`, specifying a stream from which to read. This data may take any of several forms, including PostScript, raw text, JPEG graphic, and so on. `lpr` passes the data to `lpd`, which checks the printcap file for specifics about the printer. If the printcap entry includes a filter line, `lpd` sends the data (document) through that filter as discussed earlier. Once the document is filtered, `lpd` sends it to the queue specified in the printcap entry for that printer.

Commonly used arguments to `lpr` include:

| Argument | Description |
|---|---|
| -P queue_name | Forces output to a particular printer instead of the default printer or the printer specified by the `PRINTER` environment variable. Do not include a space between -P and queue name. |
| -h | Suppresses the printing of a header page. |
| -m mail_addr | Sends mail to `mail_addr` upon completion of the print. |
| -# num | Prints `num` copies of each file. |
| -T title | Title to print on cover page. |

## lpq

The `lpq` command controls the queue examination program, which lists the print jobs currently waiting in the queue. The `lpq` command returns the user's name, the job's current place in the queue, the files that make up the print job, a numeric identifier for the job, and the total size of the job in bytes. To check the queue for a specific printer, use the `-P` option, as with the `lpr` command. To check the queue for jobs owned by a specific user, enter a username as an argument. In action, `lpq` looks like this:

```text
$ lpq -P hp4000
Printer: lp is lp@localhost
Printer: lp@speaker 'raw'
Queue: 3 printable jobs
Server: pid 12180 active
Unspooler: pid 12181 active
Status: printing 'user@speaker+179', file 1 'yac1-egcs.txt', size
4172, format 'l' at 18:06:54
Rank Owner/ID Class Job Files Size Time
active user@speaker+179 A 179 yacl-egcs.txt 4172 18:06:54
2 user@speaker+182 A 182 tweener.txt 4879 18:07:05
3 user@speaker+186 A 186 kms94.ps 125700 18:07:16
```

Note The output format of LPRng, as shown above, differs from the format of the original lpd's lpq. LPRng's listing is more complete, but lpd's provides much of the same critical information, including a job ID number and the name of the file being printed.

## lpc

The LPRng System Control program, or *lpc*, provides the capability to disable or enable a print queue, to reorder the print jobs in a queue, and to obtain status information about a printer, a queue, or a job. These commands are applicable to any printer in the */etc/printcap* file as specified by the associated name or to all printers.

If issued without an argument, the *lpc* session will be interactive and an *lpc>* prompt will be returned. You can also include the *lpc* command in a script, using the following format:

```text
lpc [subcommand]
```

The available subcommands are as follows:

-   **abort**: Terminates any printing in progress and then disables further printing to the specified printer(s). The queue is left intact so that the waiting print jobs will be printed when the *start* command is next issued. Sometimes, if a printer has stopped printing for no apparent reason, issuing the *abort* command followed by the *start* command will get things going again.
-   **disable**: Turns the queue off so that it won't accept any more jobs, although the superuser can still queue print jobs. Printing is not halted, so anything in the queue already or added by the superuser will print. When a printer is to be deactivated, you should issue the *disable* command followed by the *stop* command.
-   **down**: Turns the specified print queue off, disables printing to that queue, and logs a message to the printer status file. Subsequent attempts to run the *lpc* command will indicate that it is down and output the status message.
-   **enable**: Enables spooling on the specified printer's queue so that it will accept new jobs.
-   **exit**: Terminates the interactive *lpc* session.
-   **reread**: Tells the *lpd* daemon to reread its configuration file.
-   **start**: Enables printing and starts a spooling daemon for the specified printer(s).
-   **stop**: Stops *lpd* after the current job has been completed and disables printing.
-   **topq [printer] [jobs]**: Places the jobs in order at the top of the queue (after the currently printing job) for the specified printer(s). Unless *topq* has been used to reorder them, the jobs will be in FIFO order (first in first out).
-   **up**: Enables the queue for the specified printer and starts a new printer daemon for that queue.

As an example, suppose you want to reorder the jobs in the *lexmark* print queue so that job 186 from the earlier *lpq* example prints before job 182. (Ordinarily, job numbers are assigned in ascending order according to print order.) You might use the following command to accomplish this
