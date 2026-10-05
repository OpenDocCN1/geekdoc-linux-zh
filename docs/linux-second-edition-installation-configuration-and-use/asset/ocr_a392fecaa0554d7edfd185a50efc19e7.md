For large files, the file to be printed is spooled; lpd temporarily stores the data in a directory such as /var/spool/lpt. It is possible to execute several print commands in a row before the printing of the first file is terminated.

lpc provides you with a list of all pooled files and print jobs. The size of the file and its job number are shown. You can specify the job number as a parameter of lpc when you want to remove a file from the print spooler. Please note that all spool data is stored on the hard disk and is not lost by a restart of Linux. lpd detects whether there are files that have not been printed, and if this is the case, it keeps trying to send the data to the printer.

The lpc command allows more detailed control over the printing process. After you have started it, you find yourself in a special environment in which you can execute commands such as status, help, and so on. With topq you can place a print job at the top of the listing. You must specify the printer name and the job number as parameters. Some of the commands in lpc (for example, topq) can only be executed by root. exit, by, or terminate lpc.

# Automatic conversion into printer format

One problem we have not yet looked at is the conversion of documents into the printer format. For this purpose, lpd provides a filter concept: printcap, the command if can be used to specify a filter program. When lpd is called, the file is processed by the specified filter and the result passed to the printer. (Thus, a 'filter' is simply a process that processes input data and outputs data.) Depending on the configuration, the filter program performs two tasks:

+   - It converts files of different formats (ASCII, LTEX, *.d, and so on) into PostScript by calling different translation programs (a2ps, Latex, dvips, and so on). It is essential that the filter recognizes the file type.
- It uses gs to convert PostScript files into files in the format of the connected printer (if this printer is not a PostScript printer in the first place).

Depending on the distribution, filters of different scopes are provided, two of which will be briefly mentioned:

RedHat/Caldera offers only a filter for the conversion PostScript -> printer format or text -> printer format, thus presumably that lpd is only PostScript files for printing. The filter /var/spool/lpd/lp/filter can easily be configured with pprint.

SE uses the more versatile apsfilter, which performs both of the conversions mentioned above. It is configured with vast (ADMINISTRATION/HARDWARE PRINTER). This creates three printer interfaces, lp, raw, and ascii. raw is suitable for printing files that are already in the printer format straight to the printer without any conversion. ascii is for printing ASCII files, lp for all other files (which are then converted as needed).

apsfilter works transparently when calling lpr. If you have configured apsfilter for the HP Laserjet, the instruction lpr.file translates the DVI file into