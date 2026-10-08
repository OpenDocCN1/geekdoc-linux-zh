# 722

# lp

Note — Print jobs are assumed to contain one type of data. That type of data is either specified on the command line or autodetected (simple, PostScript) according to the contents of the first file in the job.

# Options

Printers that have a 4-x or BSD-based print server are not configured to handle BSD protocol extensions. lp handle print requests sent to such printers in the following

+   - Print requests with more than 52 file names are truncated to 52 files. lp displays a warning message.
- -f, -H, -O, -P, -q, -S, -T, and -y options may require a protocol extension to pass to a print server. If lp cannot handle the print request, it displays the following warning message.

LP administrators enable protocol extensions by setting a printer's bsdaddr in /etc/printers.conf. Changing the bsdaddr entry in /etc/printers.conf to:

```
destination:bsaddr=server, destination, Solaris
```

generates a set of BSD protocol extensions that can be processed by a Solaris print server. lp supports only Solaris protocol extensions at this time.

+   -c Copy file before printing. Unless you specify -c, you should not remove any file before the print request has completely printed. Changes made to file after the print request is made but before it is printed are reflected in the printed output. file is linked (as opposed to copied).

+   -d destination Print file on a specific destination. destination can be either a printer or a class of printers (see lpadmin(1)). Specify destination using atomic, POSIX-style(server.destination) or Federated Naming Service (FNS)(../service/printer/...) names. printersconf(4) for information regarding the naming conventions for atomic and FNS names, and standards(5) for information POSIX.

+   -f form-name Print file on form-name. The LP print server ensures that the form is mounted on the printer. The print request is rejected if the printer does not support form-name, if form-name is not defined for the system, or if the user is not allowed to use form-name(see lpforms(1)).

+   -H special-handling Print the print request according to the value of special-handling. The following special-handling values are acceptable: