
some of the SunOS stuff). For real-time notification when you are away from your terminal, you can use the `exec` and `pipe` keywords. swatch-2.2 came with some utilities that could be used in the configuration file (`badloginfinger.pl` and `call_pager.pl`), but they don't seem to be included with version 3.0. If you like, you can grab them out of the older version 2.2 or replace them with similar utilities you may already have. Our example shows a call to `badloginfinger.pl`, which will safely finger the site from which the bad login came. We also send notification of the bad login attempt to our pager via the `call_pager.pl` utility, and use the `pipe` keyword to echo output from `su` to a printer.

Because swatch reports only what you tell it to, you might want to consider keeping the report all pattern (`/.*/`) at the end of the file, carefully adding patterns to ignore as you go along. For purposes of this illustration, our configuration file will be saved in `/usr/local/etc/swatch/swatchrc.messages`. You will need to create configuration files for each log file that you want to monitor with swatch.

If our messages file is rotated every day, we can tell swatch to restart itself just after that happens. The command to continuously monitor this file, restarting every morning, might look something like this:

```
swatch -t /var/log/messages -c /usr/local/etc/swatch/swatchrc.messages -r 04:01
```

You may also invoke the restart through logrotate. Example 17-11 provides an example entry that may be placed in `/etc/logrotate.d` for `/var/log/messages`.

### Example 17-11 Restarting swatch on /var/log/messages through logrotate

```
/var/log/messages {
    prerotate
        /usr/bin/chattr -a /var/log/messages
    endscript
    postrotate
        /usr/bin/killall -HUP syslogd
        /usr/bin/chattr +a /var/log/messages
        /usr/local/etc/swatch -t /var/log/messages -c /usr/local/etc/swatch/swatchrc.messages -r +0
    endscript
}
```

Using the command and configuration file as shown in Example 17-10, we might see output similar to that in Example 17-12 echoed to our monitoring window (lines wrapped due to length).

If you update the configuration file while swatch is running, send the swatch process an ALRM or HUP signal. It will reread its configuration file and restart. swatch terminates gracefully when you send it a QUIT, TERM, or INT signal.

swatch is pretty good at making sure you receive notifications. With a little tuning of the configuration file, it should work well for you, but use additional tools as well.

### Example 17-12 Sample of Output Generated from swatch Based on Example 17-10

```
Mar 2 17:54:15 topcast login[14435]: FAILED LOGIN 1 FROM roadrunner FOR guest,  
Authentication failure
Mar 2 17:54:23 topcast login[14435]: FAILED LOGIN 2 FROM roadrunner FOR guest,  
Authentication failure
Mar 2 17:54:28 topcast login[14435]: TOO MANY LOGIN TRIES (3) FROM roadrunner FOR  
guest, Have exhausted maximum number of retries for service.
Mar 2 17:54:28 topcast PAM_pwdb[14435]: 3 authentication failures; (uid=0)  
->guest for login service
Mar 2 18:00:10 topcast login[14478]: FAILED LOGIN 1 FROM roadrunner FOR guest,  
Authentication failure
Mar 2 18:00:16 topcast login[14478]: FAILED LOGIN 2 FROM roadrunner FOR joe,  
Authentication failure
Mar 2 18:00:20 topcast login[14478]: FAILED LOGIN 2 FROM roadrunner FOR mary,  
Authentication failure
Mar 2 18:50:38 net-print.mydomain.com printer: paper out
Mar 2 18:50:38 net-print.mydomain.com printer: error cleared
Mar 2 18:50:38 net-print.mydomain.com printer: cover/door open
Mar 2 18:50:38 net-print.mydomain.com printer: error cleared
4 in 0:28:06 net-print.mydomain.com printer: paper out
4 in 0:28:06 net-print.mydomain.com printer: error cleared
4 in 0:28:06 net-print.mydomain.com printer: cover/door open
4 in 0:28:06 net-print.mydomain.com printer: error cleared
```

## logcheck

logcheck is a utility designed to periodically check the new stuff in your log files for an "unusual" item while ignoring the items you don't care about. It then mails the events of interest (if any) to you in a nice summary. logcheck's philosophy is to report known bad events (by matching keywords in a configuration file) and to report everything else it hasn't been told to ignore. While swatch can be used in a real-time fashion, you can use logcheck to receive notification of all those other log entries that may not be as time sensitive but are just as important.

logcheck comes with a helper utility that is smart enough to know when your log files have been rotated by checking the inode numbers and file size. It also keeps track of the portion of the log file that has already been processed so that you get a report only of new events (or no report if there are no events to report). logcheck should not overlook any important events, as its default behavior is to report everything you tell it to, along with everything you don't specifically tell it to ignore.

logcheck is a free clone of the `frequentcheck.sh` script distributed with the Gauntlet firewall by Trusted Information Systems, Inc. Craig H. Rowland is the author of logcheck and obtained permission from TIS to release this clone. See the LICENSE file distributed with logcheck for more information.

## Obtaining logcheck

You can obtain logcheck from its home page or COAST:

- http://www.psonic.com/abacus/logcheck/
- ftp://coast.cs.purdue.edu/pub/tools/unix/logcheck/

As of this writing, the latest version of logcheck is 1.1. To retrieve the latest version of logcheck, the author's PGP key, and the signature file for logcheck:

```
logcheck-1.1.tar.gz
logcheck-1.1.tar.gz.asc
signature-file.asc
```

Add the author's PGP signature to your keyring and verify that the signature of the package is good as shown in:

```bash
# gpg signature-file.asc
# gpg logcheck-1.1.tar.gz.asc
```

or use `pgpv` if you are using PGP Version 5.0.

## Major Components of logcheck

Major files used by logcheck, and their use, are shown in Table 17.5.

| File | Use |
|---|---|
| logcheck.sh | This is the main script that logcheck should run via cron. logcheck reads the logcheck configuration files and your log files (with help of the logtail program) to generate a report. |
| logtail | Tracks information on the log files. Remembers how much of each log file has been processed, and notes log file length and file size, which it uses to determine if log file has been rotated. The information gathered by logtail is stored in a file named log_filename.offset, in the same directory as the log file. logtail is a C program. |
| logcheck.hacking | This configuration file contains keywords that indicate a system attack. Log entries are searched to match these keywords. The search for these keywords is case insensitive. All matches will be shown at the top of your report to get your attention. This configuration file is checked first. |
| logcheck.violations | This configuration file contains patterns matching events indicating either a system problem or possible impending threat. This file is consulted after the logcheck.hacking file. The keywords in this file are also searched case insensitively. |
| logcheck.violations.ignore | The violations.ignore configuration file contains keywords similar to those found in logcheck.violations but which are ignored. logcheck will treat the keywords in this file case sensitively. Use this file carefully and make sure you don’t ignore something important. |
| logcheck.ignore | The last configuration file to be read. Any keywords listed in this file, if matched, will be ignored. The keywords in this file are also treated case insensitively. Again, be careful about specifying the pattern to ignore. |

## Configuring and Installing logcheck

Edit `systems/linux/logcheck.sh`. Find the CONFIGURATION SECTION and verify that the `SYSADMIN` variable is set so that the output will be mailed to the appropriate person (it defaults to root):

```
SYSADMIN=root
```

Review the default installation directory choices and make any changes to suit your taste. We used the defaults shown in Example 17-13. If you choose not to use the default locations for these files, you will have to edit the Makefile and modify it appropriately.

Next review the LOGFILE section in the same file. This is the place where you tell logcheck which log files you want it to examine. If you have any other files, you can add them to the end of this section. See Example 17-14 for an illustration.

After saving any changes, you are ready to install (unless you need to edit the Makefile because you customized the installation directories!). Now execute `make linux`. (The different systems come with different keyword files.) Example 17-15 shows the output generated while installing logcheck. Set up a crontab to run logcheck, maybe once an hour.

```
0 * * * * /usr/local/etc/logcheck.sh
```

Now let's take a look at the files containing the patterns logcheck looks for (or ignores). There are four files and they are read in a specific order. The files come populated with a set of keywords, but you can add your own. Please read Craig's README files before you do this—they do contain a lot of useful information.

### Example 17-13 Default Installation Directories Used by logcheck

```bash
LOGTAIL=/usr/local/bin/logtail
TMPDIR=/usr/local/etc/tmp
GREP=egrep
MAIL=mail

HACKING_FILE=/usr/local/etc/logcheck.hacking
VIOLATIONS_FILE=/usr/local/etc/logcheck.violations
VIOLATIONS_IGNORE_FILE=/usr/local/etc/logcheck.violations.ignore
IGNORE_FILE=/usr/local/etc/logcheck.ignore
```

### Example 17-14 Configuring logcheck to Monitor Specific Files

```bash
$LOGTAIL /var/log/messages > $TMPDIR/check.$$
$LOGTAIL /var/log/secure >> $TMPDIR/check.$$
$LOGTAIL /var/log/maillog >> $TMPDIR/check.$$
$LOGTAIL /var/log/critlog >> $TMPDIR/check.$$
```
