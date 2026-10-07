After reading through the printcap file and printing anything left in the queue, the line printer daemon goes into a passive mode, waiting for requests to print files, reorder print jobs in the queue, or display the waiting print jobs. It uses the system calls `listen` and `accept` to determine whether any such requests are made.

As mentioned above, the line printer daemon package includes other programs necessary to the printing functionality. These binaries perform specific functions, which we'll look at next.

# lpr

The `lpr` program is the spooling command that makes requests of `lpd`. `lpr` makes contact with the line printer daemon when it needs to put a new print job into the spool. The format is basic:

```
lpr path-to-file [arguments]
```

When you print from an application under Linux, the program runs `lpr`, specifying a stream from which to read. This data may take any of several forms, including PostScript, raw text, JPEG graphic, and so on. `lpr` passes the data to `lpd`, which checks the printcap file for specifics about the printer. If the printcap entry includes a filter line, `lpd` sends the data (document) through that filter as discussed earlier. Once the document is filtered, `lpd` sends it to the queue specified in the printcap entry for that printer.

Commonly used arguments to `lpr` include:

| -P queue name | Forces output to a particular printer instead of the default printer or the printer specified by the `PRINTER` environment variable. Do not include a space between -P and queue name. | |---|---|| -h | Suppresses the printing of a header page. || -m mail_addr | Sends mail to `mail_addr` upon completion of the print. || -# num | Prints `num` copies of each file. || -T title | Title to print on cover page. |

# lpq

The `lpq` command controls the queue examination program, which lists the print jobs currently waiting in the queue. The `lpq` command returns the user's name, the job's current place in the queue, the files that make up the print job, a numeric identifier for the job, and the total size of the job in bytes. To check the queue for a specific printer, use the `-P` option, as with the `lpr` command. To check the queue for jobs owned by a specific user, enter a username as an argument. In action, `lpq` looks like this:

```
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