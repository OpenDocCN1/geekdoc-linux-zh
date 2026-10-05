# TRADITIONAL UNIX PRINTING 559

![](bbox=[0.27, 0.09, 0.87, 0.515])

# HP_Laserjet_P2055dn (Processing, Accepting Jobs, Not Shared)

Description: HP LaserJet P2055dn

Driver: HP LaserJet P2055dn pc2, hpcups 3.10.2

Connection: http://localhost:631/printers/HP_Laserjet%20%25%8B6E5303%5D_printer_top.local/

Defaults: job sheetsnow, none mediumname, letter 8.5x11

# Jobs

| ID | Name | User Size Pages State | Control |
|---|---|---|---|---|---||
| 1 | HP_Laserjet_P2055dn-1 | | 14.10 sam | 62k Unknown | processing since Mon 12 Apr 2010 12:12:50 PM PDT | Cancel Job / Move Job |

Table 14-12 Printer page showing jobs information

# Table 14-2 BSD and System V command-line print utilities

# BSD/SysV Purpose

+   - lpr sends job(s) to the printer
- lpq/lpstat displays the status of the print queue
- lprm/cancel removes job(s) from the print queue

The preceding command adds memo.txt to the print queue of the default printer as job 25. When printer is available, it prints the file. You can specify a using the -d option:

```
$ lp -d ColorPtr graph.ps
request id is ColorPtr-26 (1 file))
```

The lp -P option is equivalent to the lp -d option.

Without arguments, lp and lpr send their standard input to the printer:

```
$ cat memo2.txt | lp
request id is MainPrinter-27 (1 file))
```

The lpq and lpstat commands display information about the print queue: