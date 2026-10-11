
## 21.14 Page Accounting with CUPS

- The PPD contains all the information needed to use our model and the driver; once installed, this works transparently for the user. Later you'll only need to choose resolution, paper size, and so on, from the Web-based menu, or from the print dialog GUI, or from the command line.

- If you ended up on the drivers page^55^, you can choose to use the “PPD-O-Matic” online PPD generator program.

- Select the exact model and check either **Download** or **Display PPD file** and click **Generate PPD file**.

- If you save the PPD file from the browser view, please do not use cut and paste (since it could possibly damage line endings and tabs, which makes the PPD likely to fail its duty), but use *Save as..* in your browser’s menu. (It is best to use the **Download** option directly from the Web page.)

- Another interesting part on each driver page is the **Show execution details** button. If you select your printer model and click on that button, a complete Ghostscript command line will be displayed, enumerating all options available for that combination of driver and printer model. This is a great way to “learn Ghostscript by doing”. It is also an excellent cheat sheet for all experienced users who need to reconstruct a good command line for that darned printing script, but can’t remember the exact syntax.

- Sometimes during your visit to Linuxprinting.org, save the PPD to a suitable place on your hard disk, say `/path/to/my-printer.ppd` (if you prefer to install your printers with the help of the CUPS Web interface, save the PPD to the `/usr/share/cups/model/` path and restart cupsd).

- Then install the printer with a suitable command line, like this:

```
root# lpadmin -p laserjet4plus -v parallel:/dev/lp0 -E \
-P path/to/my-printer.ppd
```

- For all the new-style “Foomatic-PPDs” from Linuxprinting.org, you also need a special CUPS filter named foomatic-rip.

- The foomatic-rip Perl script itself also makes some interesting reading^56^ because it is well documented by Kamppeter’s in-line comments (even non-Perl hackers will learn quite a bit about printing by reading it).

- Save foomatic-rip either directly in `/usr/lib/cups/filter/foomatic-rip` or somewhere in your `$PATH` (and remember to make it world-executable). Again, do not save by copy and paste but use the appropriate link or the **Save as..** menu item in your browser.

- If you save foomatic-rip in your `$PATH`, create a symlink:

```
55: http://www.linuxprinting.org/show_driver.cgi?driver=ljet4>
56: http://www.linuxprinting.org/foomatic2.9/download.cgi?filename=foomatic-rip&show=1>
```

```
root# cd /usr/lib/cups/filter/ ; ln -s '`which foomatic-rip`'
```

CUPS will discover this new available filter at startup after restarting cupsd.

Once you print to a print queue set up with the Foomatic PPD, CUPS will insert the appropriate commands and comments into the resulting PostScript job file. foomatic-rip is able to read and act upon these and uses some specially encoded Foomatic comments embedded in the job file. These in turn are used to construct (transparently for you, the user) the complicated Ghostscript command line telling the printer driver exactly how the resulting raster data should look and which printer commands to embed into the data stream. You need:

- A “foomatic+something” PPD — but this is not enough to print with CUPS (it is only *one* important component).
- The *foomatic-rip* filter script (Perl) in `/usr/lib/cups/filters/`.
- Perl to make foomatic-rip run.
- Ghostscript (because it is doing the main work, controlled by the PPD/foomatic-rip combo) to produce the raster data fit for your printer model’s consumption.
- Ghostscript *must* (depending on the driver/model) contain support for a certain device representing the selected driver for your model (as shown by `gs -h`).
- foomatic-rip needs a new version of PPDs (PPD versions produced for cupsomatic do not work with foomatic-rip).

Often there are questions regarding print quotas where Samba users (that is, Windows clients) should not be able to print beyond a certain number of pages or data volume per day, week, or month. This feature is dependent on the real print subsystem you're using. Samba's part is always to receive the job files from the clients (filtered or unfiltered) and hand them over to this printing subsystem.

Of course one could hack things with one's own scripts. But then there is CUPS. CUPS supports quotas that can be based on the size of jobs or on the number of pages or both, and can span any time period you want.

### 21.14.1 Setting Up Quotas

This is an example command of how root would set a print quota in CUPS, assuming an existing printer named "quotaprinter":

```
root# lpadmin -p quotaprinter -o job-quota-period=604800 \
-o job-k-limit=1024 -o job-page-limit=100
```

This would limit every single user to print no more than 100 pages or 1024 KB of data (whichever comes first) within the last 604,800 seconds (= 1 week).

### 21.14.2 Correct and Incorrect Accounting

For CUPS to count correctly, the printfile needs to pass the CUPS pstops filter; otherwise it uses a dummy count of “one”. Some print files do not pass it (e.g., image files), but then those are mostly one-page jobs anyway. This also means that proprietary drivers for the target printer running on the client computers or CUPS/Samba, which then spool these files as “raw” (i.e., leaving them untouched, not filtering them), will be counted as one-pagers too!

You need to send PostScript from the clients (i.e., run a PostScript driver there) to have the chance to get accounting done. If the printer is a non-PostScript model, you need to let CUPS do the job to convert the file to a print-ready format for the target printer. This is currently working for about a thousand different printer models. Linuxprinting.org has a driver list^{57}.

### 21.14.3 Adobe and CUPS PostScript Drivers for Windows Clients

Before CUPS 1.1.16, your only option was to use the Adobe PostScript driver on the Windows clients. The output of this driver was not always passed through the pstops filter on the CUPS/Samba side, and therefore was not counted correctly (the reason is that it often, depending on the PPD being used, wrote a PJL-header in front of the real PostScript, which caused CUPS to skip pstops and go directly to the pstoraster stage).

From CUPS 1.1.16 and later releases, you can use the CUPS PostScript driver for Windows NT/200x/XP clients (which is tagged in the download area of http://www.cups.org/ as the cups-samba-1.1.16.tar.gz package). It does not work for Windows 9x/Me clients, but it guarantees:

- To not write a PJL-header.
- To still read and support all PJL-options named in the driver PPD with its own means.
- That the file will pass through the pstops filter on the CUPS/Samba server.
- To page-count correctly the print file.

You can read more about the setup of this combination in the man page for cupsaddsmb (which is only present with CUPS installed, and only current from CUPS 1.1.16).

### 21.14.4 The page.log File Syntax

These are the items CUPS logs in the page.log for every page of a job:

57<http://www.linuxprinting.org/printer_list.cgi>

- Printer name
- User name
- Job ID
- Time of printing
- Page number
- Number of copies
- A billing information string (optional)
- The host that sent the job (included since version 1.1.19)

Here is an extract of my CUPS server’s `page_log` file to illustrate the format and included items:

```
tec_IS2027 kurt 401 [22/Apr/2003:10:28:43 +0100] 1 3 #marketing 10.160.50.13
tec_IS2027 kurt 401 [22/Apr/2003:10:28:43 +0100] 2 3 #marketing 10.160.50.13
tec_IS2027 kurt 401 [22/Apr/2003:10:28:43 +0100] 3 3 #marketing 10.160.50.13
tec_IS2027 kurt 401 [22/Apr/2003:10:28:43 +0100] 4 3 #marketing 10.160.50.13
Dig9110 boss 402 [22/Apr/2003:10:33:22 +0100] 1 440 finance-dep 10.160.51.33
```

This was job ID *401*, printed on `tec_IS2027` by user *kurt*, a 64-page job printed in three copies, billed to `#marketing`, and sent from IP address 10.160.50.13. The next job had ID *402*, was set by user *boss* from IP address 10.160.51.33, printed from one page 440 copies, and is set to be billed to `finance-dep`.

### 21.14.5 Possible Shortcomings

What flaws or shortcomings are there with this quota system?

- The ones named above (wrongly logged job in case of printer hardware failure, and so on).
- In reality, CUPS counts the job pages that are being processed in *software* (that is, going through the RIP) rather than the physical sheets successfully leaving the printing device. Thus, if there is a jam while printing the fifth sheet out of 1,000 and the job is aborted by the printer, the page count will still show the figure of 1,000 for that job.
- All quotas are the same for all users (no flexibility to give the boss a higher quota than the clerk) and no support for groups.
- No means to read out the current balance or the "used-up" number of current quota.
- A user having used up 99 sheets of a 100 quota will still be able to send and print a 1,000 sheet job.
- A user being denied a job because of a filled-up quota does not get a meaningful error message from CUPS other than "client-error-not-possible".
