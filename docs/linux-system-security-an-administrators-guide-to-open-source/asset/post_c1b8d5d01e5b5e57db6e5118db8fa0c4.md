
## Example 17-5 Overriding Default Directives in an Included File (Continued)

```
prerotate
/usr/bin/chattr -a /var/log/netconf.log
endscript
postrotate
/usr/bin/chattr +a /var/log/netconf.log
endscript
}

/var/log/boot.log {
  nocompress
  monthly

  prerotate
    /usr/bin/chattr -a /var/log/boot.log
  endscript
  postrotate
    /usr/bin/chattr +a /var/log/boot.log
  endscript
}
```

## Pulling It All Together

There’s not a lot of work required to install and run logrotate. Basically, all you have to do is identify your log files, create rotation directives for them, and run logrotate through cron. By default, Red Hat ships with the crontab shown in Example 17-6 to accomplish this.

## Example 17-6 logrotate crontab run from /etc/cron.daily

```
# cat /etc/cron.daily/logrotate
#!/bin/sh

/usr/sbin/logrotate /etc/logrotate.conf
```

## swatch

swatch (the simple watchdog) is a program designed to keep an eye on your log files and to notify you when interesting events occur. You can run swatch in batch mode—you examine a log file’s contents and exit—or in monitor mode—swatch continuously watches the log file, evaluating each new record (tailing the file). swatch can provide notification in a more real-time fashion than logcheck. A drawback, however, is that you need to have a swatch process running on each machine you wish to monitor and for each log file, which can be cumbersome if you do not log your files to a central machine.

swatch was written and is maintained by E. Todd Atkins, who distributes swatch under the GPL. swatch-3.0 provides a variety of notification options (seven colors if your terminal provides that support, terminal bell, e-mail, messages to your terminal window, etc.) and offers greater ease of configuration over swatch Version 2. If you already have configuration files written for swatch Version 2, the Version 3 release has a compatibility mode to read the older-style configuration files and a utility you can use to convert the older-format files to the new format.

### Obtaining swatch

swatch can be found at its official home site or at the COAST archive

```
ftp://ftp.stanford.edu/general/security-tools/swatch/
ftp://coast.cs.purdue.edu/pub/tools/unix/swatch/
```

From the ftp site, you will need the following files (or the latest version available):

- FILES
- swatch.tar.asc
- swatch-3.0.tar.gz

The FILES file contains information about retrieving the PGP key used to sign the distribution.

You can retrieve the PGP key from a link off of the http://www.stanford.edu/~security page. Download the public key (we’ll call it stanford-security-pgp.asc), add the key to your PGP keyring, and verify that the signature is good (or use pgpv if you use PGP version 5).

```
# pgp stanford-security-pgp.asc
# pgp swatch.tar.asc
```

swatch-3.0 requires Perl 5 or greater and the following Perl modules:

- Time::HiRes
- Date::Calc
- File::Tail

If you don’t have the required Perl modules already installed on your system, the swatch installation script will attempt to install them for you automatically from one of the Comprehensive Perl Archive Network (CPAN) sites. Failing this, you can install them yourself.

Unzip and untar to reveal files as shown in Example 17-7. As always, read the usual files (COPYING, README, etc.) to learn the details about this program (especially KNOWN_BUGS).

## Example 17-7 Contents of swatch Distribution

```
CHANGES
COPYING
COPYRIGHT
INSTALL
KNOWN_BUGS
MANIFEST
Makefile.PL
README
README.Y2K
examples/
swatch
swatch_oldrc2newrc
t
```

1. See the home page at http://www.cpan.org/ for more information.

Since the installation script can attempt to install Perl modules from CPAN, you may want to read the following brief overview of CPAN before starting. If you've already used CPAN, feel free to skip ahead to the next section.

## Oh, By the Way...

There are hundreds of CPAN sites, but they are all mirrors of one master site. The mirrors exist so you can find a site close to you from which you can retrieve all things Perl. The Perl modules are libraries written for a prescribed purpose, contributed by people on the net. You can write and contribute your own, if you wish. One such module is CPAN.pm. This module can be used in Perl programs to help you install other modules your program might need. However, you should read the following statement on security at CPAN.

### SECURITY

There's no strong security layer in CPAN.pm. CPAN.pm helps you to install foreign, unmasked, unsigned code on your machine. We compare to a checksum that comes from the net just as the distribution file itself. If somebody has managed to tamper with the distribution file, they may have as well tampered with the CHECKSUMS file. Future development will go towards strong authentication.

If you do choose to use the CPAN.pm module to automatically install modules, you should at least install the MD5 module at your site so that the CPAN.pm module can verify the signature of the package you are downloading. You can find the MD5 module (and a README file explaining how to install it) at a CPAN site in the directory

```
modules/by-module/MD5/
```

If you can't get the CPAN.pm module to work, you can still FTP the required modules and signatures from a CPAN site, verify them yourself, and place them in your Perl library directory (/usr/lib/perl5 on Red Hat).

When you run the CPAN.pm module, it will ask you questions about your preferences on CPAN sites. Example 17-8 shows a sample of the dialog, snipped for brevity. Since there are many mirrors, you can choose a site close to you. See the CPAN home page for more information.

## Installing swatch

swatch is fairly simple to install. Begin by executing `perl Makefile.PL`, as shown in Example 17-8. There's a lot of dialog from the CPAN.pm module as it attempts to locate the server and as it retrieves the modules. You have to go through the CPAN.pm configuration dialog only one time, and then your preferences are saved for next time.

## Example 17-8 Sample CPAN.pm Dialog during perl Makefile.PL

```
# perl Makefile.PL

# /usr/lib/perl5/CPAN/Config.pm initialized.
The CPAN module needs a directory of its own to cache important
index files and maybe keep a temporary mirror of CPAN files. This may
be a site-wide directory or a personal directory.

First of all, I'd like to create this directory. Where?
CPAN build and cache directory? [/home/root/.cpan|/root/.cpan]
If you want, I can keep the source files after a build in the cpan
home directory. If you choose so then future builds will take the
files from there. If you don't want to keep them, answer 0 to the
next question.

How big should the disk cache be for keeping the build directories
with all the intermediate files?
Cache size for build directory (in MB)? [10]
The CPAN module will need a few external programs to work
properly. Please correct me, if I guess the wrong path for a program.
Don't panic if you do not have some of them, just press ENTER for
those.

Where is your gsisp program? [/usr/bin/gzip]
Where is your tar program? [/bin/tar]
Where is your unzip program? [/usr/bin/unzip]
Where is your make program? [/usr/bin/make]
Where is your lnxx program? [/usr/bin/lnxx]
Where is your ncftp program? [/usr/bin/ncftp]
Where is your ftp program? [/usr/bin/ftp]
What is your favorite pager program? [/usr/bin/less]
What is your favorite shell? [/bin/tcsh]
Every Makefile.PL is run by perl in a separate process. Likewise we
run 'make' and 'make install' in processes. If you don't want to pass to
the calls, please specify this here.
(e.g., PREFIX, INSTALLPREFIX, UNINST or the like) you want to pass to
the calls, please specify this here.

If you don't understand this question, just press ENTER.
Parameters for the 'perl Makefile.PL' command? []
Parameters for the 'make' command? []
Parameters for the 'make install' command? []
  Sometimes you may wish to leave the process running by CPAN alone
without caring about them. As sometimes the Makefile.PL contains
question you're expected to answer, you can set a timer that will
kill a 'perl Makefile.PL' process after the specified time in seconds.
If you set this value to 0, these processes will wait forever. This is
the default and recommended setting.

Timeout for inactivity during Makefile.PL? [0]
We need to know the URL of your favorite CPAN site.
Please enter it here: ftp://ftp.fu-berlin.de/pub/languages/perl/CPAN
Testing 'ftp://ftp.fu-berlin.de/pub/languages/perl/CPAN' ...
Listing '/usr/bin/ftp' -n'
Local directory now /root/.cpan/sources
GOT '/root/.cpan/sources/MIRROR0s'
  ftp://ftp.fu-berlin.de/pub/languages/perl/CPAN' seems to work
WAIT support is available as a plugin. You need the CPAN::WAIT module
to actually use it. But we need to know your favorite WAIT server. If
you don't know a WAIT server near you, just press ENTER.
Your favorite WAIT server? [wait://i.is6.informatik.uni-dortmund.de:1404]
If you're accessing the net via proxies, you can specify them in the
CPAN configuration or via environment variables. The variable in the
the $SPAN::Config takes precedence.
Your ftp_proxy?
Your no_proxy?
commit: wrote /usr/lib/perl5/CPAN/Config.pm
Checking for Date::Calc ::
You don't have the Date::Calc module installed.
Would you like to install the module now ?
I issuing "/usr/bin/ftp -n"
```
