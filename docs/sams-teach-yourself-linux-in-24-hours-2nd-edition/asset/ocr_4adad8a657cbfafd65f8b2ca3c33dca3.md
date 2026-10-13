# Sending and Receiving Faxes

If your modem supports fax protocols, chances are that you can send and receive faxes using OpenLinux. Sending and receiving faxes under OpenLinux involves graphics translation of both received files and files you want to send. Your OpenLinux distribution on the CD-ROM contains the efax family of fax software and documentation. Have your modem's documentation on hand and read the efax manual pages and documentation under the /usr/doc/efax directory carefully before you start.

# Faxing with the efax System

The efax system, by Ed Casas, is a simple and easy-to-use fax system that, according to its documentation, is best suited to a single-user, standalone Linux system. This software consists of a series of programs and scripts and supports Class 1 and 2 fax modems.

The system is made up of the following programs:

+   - `/usr/bin/efax`—The faxing program
+   - `/usr/bin/efix`—A graphics conversion program used to prepare text files for faxing or to convert files to different graphics formats
+   - `/usr/bin/fax`—A shell script used to create, send, receive, display, or print fax files

If you want to preview or fax PostScript graphics files, you also need to have the gs PostScript interpreter and companion viewer, gv, installed on your system. For viewing received faxes, you can use the X11 client xv (discussed in Hour 16, “Graphics Tools”).

![](bbox=[0.07, 0.72, 0.18, 0.82])

> You need to edit the /usr/bin/fax script to configure faxing. But before you make changes to the script, do yourself a favor and make a copy first. If you make errors or delete the file, you need a copy to reinstall the efax software.

Before you start sending or receiving faxes, take a look at the /usr/bin/fax shell script. This program is the front-end to fax service with efax, but you need to check several sections in the file to make sure the script is configured properly. For example, the first section lists the names of the efax programs:

```
FAX=/usr/bin/fax
EFAX=/usr/bin/efax
EFIX=/usr/bin/efix
```

![](bbox=[0.9, 0.3, 0.99, 0.5])