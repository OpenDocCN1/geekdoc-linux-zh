
For the two *nameserver address* values, use the IP address of the nameserver machines, as given to you by your ISP. The second is optional—most ISPs have more than one designated nameserver as a backup in the event that the first system becomes unavailable.

Make sure that your user account has membership to the **dialout** group; otherwise, the superuser account will have to start and stop PPP, which is not recommended (see Recipe A.6.3 [Letting Users Access Hardware Peripherals], page 718).

Once you've done these things, you should be able to start and stop PPP connections to the Internet. Complete documentation for setting up PPP is in the `/usr/share/doc/ppp` directory.

## 31.1.2 Starting a PPP Connection

Once PPP has been installed and configured, use the **pon** tool to start a PPP connection to the Internet. It calls the number of your ISP with your modem, sends the appropriate login information, and starts the PPP connection.

After a PPP connection has been established, you can access the WWW or other network services, as described in the following chapters.

⇒ To start a PPP connection, type:

```
$ pon [RET]
```

**NOTES:** To make PPP automatically start when the system first boots, rename the file `/etc/ppp/no_ppp_on_boot` to `/etc/ppp/ppp_on_boot`. (You must be **root**, the superuser, to do this.)

## 31.1.3 Stopping a PPP Connection

Use the **poff** tool to stop a PPP connection. It disconnects your computer from your ISP and hangs up the modem.

⇒ To stop a PPP connection, type:

```
$ poff [RET]
```

If you ever accidentally run **pon** when a PPP connection is already established (it happens), **poff** will not work as expected because there are multiple PPP connections running. Use the **-a** option to stop all PPP connections.

⇒ To stop all PPP connections, type:

```
$ poff -a [RET]
```

## 31.1.4 Viewing the PPP Log

Use plog to output the last few lines of the PPP log file. This is useful for checking the progress of your PPP connection when it first dials.

⇒ To view the latest entries in the PPP log file, type:
    $ plog [RET]

NOTES: You need to be a member of the adm group in order to view the log file (see Recipe A.6.3 [Letting Users Access Hardware Peripherals], page 718).

## 31.2 Faxing

Efax
DEB: efax
RPM: efax
WWW: http://www.cce.com/efax/

If you have a Class 1 or 2 fax modem, you can send and receive fax ("facsimile") messages with your Linux system. The following recipes show how to do this with the efax package, which is designed for single user systems or relatively simple fax configurations (more complicated tools for faxing exist, but they are beyond the scope of this book).

To set up efax for faxing, edit the file /etc/efax.rc (you must be root to do this). The important things to specify in this file are the value for "DEV," which is the device name in /dev of the fax or modem device (this should almost always be "modem"), and the values for "FROM" and "NAME"—the fax number and organization name to appear on outgoing faxes.

NOTES: Unless you have membership to the dialout group, you must ask your system administrator for access to the modem hardware before you can use it (see Recipe A.6.3 [Letting Users Access Hardware Peripherals], page 718).

More information on faxing is contained in the Fax Server mini-HOWTO (see Recipe 2.8.6 [Reading System Documentation and Help Files], page 50).

### 31.2.1 Sending a Fax

Use efax to send a fax. It dials the telephone number you give and faxes the contents of the file or files you specify. You can send plain text files or files in TIFF Group 3 format as they are. You can also send files in other formats, but

you must convert them to TIFFG3 format first—see Recipe 31.2.4 [Converting to and from Fax Format], page 604.

Use the -d option to specify the full path name of the fax device (usually /dev/modem if you are using the modem connected to your system), and use the -t option followed by a telephone number to specify the number to send the fax to. To specify DTMF tone dialing, precede the phone number with a "T"; specify pauses in the dialing sequence with a comma character (, )—particularly useful for dialing out from a PBX or office phone system.

⇒ To fax a copy of the file resume.txt to the number 555-9099, using DTMF tone dialing, type:

```
$ efax -d /dev/modem -t T555-9099 resume.txt [RET]
```

To send more than one file, specify them as arguments in the order they are to be sent. You can also specify them with a wildcard character, but be careful—they are sent in the order in which the shell expands the file names, which is alphabetical order. If you have a lot of files that should be sent in a particular order, rename them so their file names begin with the number of the page they correspond to. But be sure to number them with the same number of digits for each file—for example, if you have 11 files to fax, don't name them 1.fax, 2.fax, and so on, to 10.fax and 11.fax, because the shell will expand them in the order of 1.fax, 10.fax, 11.fax, 2.fax, 3.fax, and so on up to 9.fax. In this case, you would number them as 01.fax, 02.fax, and so on, so that files 1 through 9 contain the same number of digits in their names as do 10.fax and 11.fax.

⇒ To fax all of the files with the .fax extension in the current directory to the number 555-9099, using DTMF tone dialing, type:

```
$ efax -d /dev/modem -t T555-9099 *.fax [RET]
```

Another way to do this is to make a text file containing the list of files to fax, one file name per line, in the order you want them sent. If the files you want to send are not in the current directory, be sure to write the file names with path names relative to the current directory—so for example, if you want to send the file header.fax, which is in your home directory, and the current directory is ~/documents/faxes, the file should be specified as ~/header.fax.

⇒ To fax all of the files listed in the file fax.list to the number 555-9099, dialing a 9 first to obtain an outside line, and using DTMF tone dialing, type:

```
$ efax -d /dev/modem -t T9,555-9099 $(cat fax.list) [RET]
```

NOTES: The efax tool doesn't delete the files it faxes.
