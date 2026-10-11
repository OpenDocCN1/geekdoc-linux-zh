# Configuring the /etc/printcap file

The /etc/printcap file is used to define the printers available to the system, whether they are local or remote on the network. The format for this file is as follows:

```
printer_name|alias_name:
    :definitions:
    :last_definition;
```

Any line that does not start with a colon or a pipe designates the beginning of a printer definition. Each line of a printer definition ends in a \\, except for the last one, which ends in a semicolon. Multiple printers can be configured in the file, each with their own definition block. A # designates a comment. The following is an example printcap file.

```
#REMOTE POSTSCRIPT 300x300 letter {} PostScript Default l
lp|hp|lj:
    :sd=/var/spool/lpd/lp:
    :mx#0:
    :sh:
    :rm=192.168.1.12:
    :rp=hp|lj:
    :if=/usr/share/printtool/master-filter:
```

After the printer name and optional aliases, there are several definitions that configure the printer. Table 12-1 lists the most common definitions. These are probably the only ones you will ever see, but the printcap man page lists them all.

![](bbox=[0.12, 0.63, 0.18, 0.67])

> Exam Tip You should restart the lpd daemon any time you make a change to the /etc/printcap file.

Table 12-1
/etc/printcap Definitions
| Definition | Function | Arguments | Example |
| :--- | :--- | :--- | :--- |
| if | Defines the input filter that formats the data before it is sent to the printer. | The path and filename of the filter | :if=/usr/share/printtool/master-filter: |
| lf | Defines the printer error log file. | The path to the log file. | :lf=/var/spool/lpd/hp|lj/errorlog:\\ | 
| lo | Defines the lock file that is created when the printer is in use. | Path to the lock file. | :lo=/var/spool/lpd/hp|lj/hp|lj.lock:\\ |