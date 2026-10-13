
## Filters

Filters translate what you want to print from your applications and editors to the various languages that a printer can understand. The two major printer graphic languages are Hewlett Packard's PCL and Adobe's PostScript. These languages fall into different categories; some applications use PostScript to translate your files to PCL. There are three major types of graphic filters that work with these languages: enscript, ghostscript, and magic. You need to set up the filter that you'll use in your /etc/printcap file.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_195_0.png)

> Most Linux applications work with PostScript files. Linux drivers for PostScript printers are more common as a result.

Enscript is a GNU clone of the commercially available enscript printer filter. Like its GNU cousin, a2ps, it converts text into PostScript format. Both enscript and a2ps are more flexible than other PostScript filters because they allow you to print two pages of text on a single sheet.

Ghostscript is a PostScript interpreter, which allows Linux to display PostScript files in graphical user interfaces, as well as a translator, which sends PostScript data to many printers.

Magic filters aren't really filters at all. They are scripts that automatically detect the type of data inside a file, and then call up the appropriate filter to convert the data for your printer. In a way, this works like the file command from Chapter 8. Magic filters convert from modes like DVI or PostScript to Hewlett Packard's PCL.

Note: DVI files are the processed data from LaTeX or TeX input files.

There is also one major filter, known as lpf. This is a filter for text files. The lpf filter reformats ASCII text to avoid "stair-stepping," when printers add an extra line after every word.

## Spool Directories

Print spools are generally located in the /var/spool/lpd directory. Each job gets its own file. On older Linux systems that use the BSD (Berkeley Standard Distribution) version of the line printer daemon, Linux can't handle spool files larger than 1MB, which is the reason for the lpr -s command. If you have trouble managing your spool with commands like lprm and lpc, you may be able to kill print jobs directly by deleting files in your spool directory.

Print spools, like log files, are normally stored in the /var directory or one of its subdirectories.

## The /etc/printcap File

All of the settings for different printers are stored in the /etc/printcap file. In this section, you'll analyze a typical /etc/printcap file, with a view towards making it work for you. An example of the /etc/printcap file from the Corel Linux distribution is shown in Figure 9.3.

This file can be rather confusing at first glance, so let's start by reviewing some of the codes available for this file. You'll then be able to interpret this file or the one currently in your Linux distribution.

### /etc/printcap codes

The codes in the /etc/printcap file can be divided into the following categories: printer names, filters, spools, log files, and special printer codes. There is also a format for separate entries in this file. For example, the first section shown in Figure 9.3 may be shown as three long code lines:

```
lp|Generic dot-matrix printer entry:lp:/dev/lp0:\
sd=/var/spool/lpd/lp:af=/var/log/lp-acct:\
lf=/var/log/lp-errs:pl#66:pw#80:pc#150:mx#0:sh
```

```
# /etc/printcap: printer capability database. See printcap(5).
# You can use the filter entries df, tf, cf, gf etc. for
# your own filters. See /etc/filter.ps, /etc/filter.pcl and
# the printcap(5) manual page for further details.

lp|Generic dot-matrix printer entry\
:lp=/dev/lp0\
:sd=/var/spool/lpd/lp\
:af=/var/log/lp-acct\
:lf=/var/log/lp-errs\
:pl#66\
:pw#80\
:pc#150\
:mx#0\
:sh\

# rlp|Remote printer entry\
# :lp=\
# :rm=remotehost\
# :rp=remoteprinter\
# :sd=/var/spool/lpd/remote\
# :mx#0\
# :sh
```

Figure 9.3 A typical /etc/printcap printer configuration file.

Unfortunately, this type of code management can make life more difficult for all but the most knowledgeable of Linux administrators. The way you set up and present code in this file or any other program helps communicate your intent to other administrators. There are three punctuation marks that help you manage /etc/printcap code.

- **Colon (:)**—Colons divide code lines. If you see a colon, even inside a line, it starts a new command.
- **Backslash (\ )**—If a line ends with a backslash, it means that the code continues onto the next line. Recall from Chapter 7 that backslash tells the shell to ignore characters like empty spaces, carriage returns, and so on.
- **Pipe (|)**—Lines after a pipe in the /etc/printcap file are comments. As you can see, the ones shown in the preceding code lines and in the figure describe some type of printer. But these comments are significant because you can use them to specify a particular printer.

> Note: The first line in a /etc/printcap paragraph usually defines a printer. You can see that the line shown previously starts with lp, which is the code for the default printer.

Printer names are based on the drivers installed and available in your /dev/ directory. Typical printer names include lp, lp1, lp2, sp1, and lf1.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_197_0.png)

> The default printer has the lp label in the /etc/printcap file. If there is no printer with this label, the first printer in this file becomes the default.

The print filters discussed earlier can be assigned as input filters (if) or output filters (of). If you have multiple print jobs on a single printer, only the input filter is used on every print job. The output filter is applied only to the first of a series of print jobs.

The spool directory (sd) is where the filtered print jobs are stored before they're sent to the printer. Linux needs a place to store these print jobs because printers aren't always available. For example, your printer could be disconnected or busy with another print job. Also, it can take time for Linux to contact printers on remote computers.

When you print, Linux can keep track of print costs and print errors. The log files dedicated to these functions are the accounting filter (af) and the line filter (lf). The accounting filter is self-explanatory. The line filter collects errors.

There are also a number of other codes. Some of the more important codes are documented in Table 9.5.

Table 9.5 Special codes for the /etc/printcap file.

| Code | Function |
|------|----------|
| rm | Remote machine: Set this equal to the hostname or IP address of the remote print server (for example, the rm=192.168.0.66 command tells the line printer daemon [lpd] that your remote printer's IP address is 192.168.0.66). |
| rp | Remote printer: If you're printing a PostScript file and your printer cannot detect this type of file, set this value equal to raw (rp=raw). |
| mx | Maximum file size: Helps you work with the older BSD line printer daemon (lpd). If you do not want a maximum file size, set this value to 0 (mx=0). |
| pw | Page width, in characters: The standard page width on U.S. letter size paper is 80 (pw#80). |
| pl | Page length, in number of lines: The standard page length on U.S. letter size paper is 66 (pl#66). |
| sh | Suppress header: When you see this command, your printer won't print a page with the job and user name. |

*Note: Much more information on the syntax inside the /etc/printcap file is available on its man page.*

## A Typical /etc/printcap File

Once you know the basic syntax, you can read most typical /etc/printcap files. Return to Figure 9.3. You know that lp is the name of the default printer, and its device is located in the device file /dev/lp0. Files that you send to this printer are first spooled in the directory defined by sd, which is /var/spool/lpd/lp:.

In a similar vein, the output from the accounting filter is stored in the /var/log/lp-acct file. Errors are taken by the line filter and sent to the /var/log/lp-errs file. The page length (pl) is 66 lines. The page width (pw) is 80 characters. The price code (pc) is 1.5 cents per page. There is no limit on the size of the printer spool file (mx#0). The suppress header (sh) command keeps the printer from printing a page with your user name and print job number.

You'll look at other examples in the practice questions.
