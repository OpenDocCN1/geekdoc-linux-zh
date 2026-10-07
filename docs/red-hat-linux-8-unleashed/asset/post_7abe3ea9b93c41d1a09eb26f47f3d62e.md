
http://www.tld.org/HOWTO/LILO-crash-rescue-HOWTO.html—This HOWTO describes how to use floppy-based recovery disks, but the general techniques are universal. The techniques covered include checking the integrity of the target filesystem. It's a little thin in content, but it is notable for its related URL links.

http://www.backupcentral.com/amanda.html—This is the Amanda chapter of UNIX Backup and Recovery available online; the site features a search tool for the chapter.

# PART III

# System Services
Administration

# IN THIS PART

+ * CHAPTER 12 Printing Services 359
* CHAPTER 13 Network Connectivity 389
* CHAPTER 14 Managing DNS 445
* CHAPTER 15 Internet Connectivity 485
* CHAPTER 16 Apache Web Server Management 503
* CHAPTER 17 Administering Database Services in Red Hat Linux 551
* CHAPTER 18 Secure File Transfer Protocol (FTP) Service 581
* CHAPTER 19 Handling Electronic Mail 627
* CHAPTER 20 News and Other Collaborative Communication 659

# CHAPTER 12

# Printing Services

# IN THIS CHAPTER

- Overview of Red Hat Linux Printing
- Configuring and Managing Print Services
- Creating and Configuring Local Printers
- Creating Network Printers
- Console Print Control
- Using the Common Unix Printing System (CUPS)
- Avoiding Printer-Support Problems
- Reference

Red Linux supports more than 600 printers from more than 40 manufacturers, and it is possible to mix and match printing hardware with newer computers. In this chapter, you learn about printing services offered in Red Hat Linux. You'll see that Linux can be put to work right away as a print platform, for use by local or remote Linux, UNIX or Windows workstations.

You learn about the many programs, files, and directories that are internal to supporting printing under Red Hat Linux. The chapter also shows simple techniques for configuring new printers in Red Hat Linux. You learn a variety of methods for making printers available for use quickly and easily in Red Hat Linux, and you learn some important workarounds for connecting printer and system hardware with differing port configurations.

Red Hat provides two different print systems you can use to print files: LPRng and the Common Unix Printing System (CUPS). You can use one or the other, but not both as the basis for printing when using Red Hat. This chapter focuses on using LPRng, but a section is devoted to setting up, configuring, administering, and using CUPS for printing. You can switch back and forth between LPRng and CUPS by using Red Hat's graphical redhat-switch-printer utility (discussed later in this chapter).

# Overview of Red Hat Linux Printing

Red Hat's new and revised print filter system is the main engine that enables the printing of many types of documents using Linux. The heart of engine is the GNU GPL version of Aladdin, Inc.'s gs client. The Red Hat system administrator's printer configuration tool is the redhat-config-printer client.

# CHAPTER 12 Printing Services

> NOTE
Hat's print system can be used to print to local (attached) or remote (network) printers. If you use a local printer, it is represented by a printer device, such as /dev/lpd0 or /dev/usb/lpd0 (if you have a USB printer). Local and remote printer definitions, known as print queues, are contained in your system's printer capabilities database, /etc/printcap. Each printer listed in this database will have a corresponding print queue spool, under /var/ spool/lpd with the printer's queue name. A document being printed is known as a print job, and you can view a list of, queue, or current print jobs in the spool directory.

To add a printer to your Red Hat Linux system, use the redhat-config-printer client to create, configure, and define the printer. The client saves the definition as an entry in your system's printer capabilities database, /etc/printcap. Each definition contains a text field that points to related and appropriately named spool directory under /var/ spool/lpd. This spool directory will hold copies of printed documents to await printing.

Along with the spool directory, the printer's printcap listing contains an entries that points to /usr/share/printconf/util/mf/wrapper. This file is a script that calls the /usr/bin/magicfilter-t utility.

A sample printer description with an if: filter entry (the shell script pointer that calls the utility) looks like this:

```
lpd:
:ml0:\
:mx#:\
:sd=/var/sp/lpd/lp:\n:af=/var/sp/lpd/lp/lpd.acct:\n:sh:
:lp=/dev/lpd0:
:lpd_bounce=true:\n:if=/usr/share/printconf/util/mf_wrapper:
```

In this example, the mf_wrapper filter utility is used as a printer filter, used to transform the printed document into an acceptable form when mf_wrapper calls a related utility (magicfilter-t) to identify the file stream as a text file, document, or image, according to initial-byte headers, or magic values, as listed in the file /usr/share/printconf/mf.magic.

> NOTE
These magic values are contained in the first bytes of many documents. They are used by the file command, which can display a file's type even if the filename is an extension. For example, PostScript documents normally have a filename extension of .ps. However, if the extension is missing, the document's format may not be readily apparent. The file command can be used to determine one or more file types like so:

# Configuring and Managing Print Services

$ file tiger art_collection
tiger: PostScript document text conforming to level 2.0 - type EPS
art_collection: Zip archive data, at least v2.0 to extract

In this example, the file named tiger is a PostScript document, whereas the file named art-collection is a compressed archive.

The magicfilter-t utility then governs the stream to PostScript, using filter rules located
at the /usr/share/printconf/mf_rules directory.
The values returned by these filter rules assign proper arguments to the Ghostscript
PostScript interpreter, gs, according to the type of destination printer. The interpreter
reads the input file as PostScript and then converts the stream to the format or
language understood by the destination printer. The data stream, using Printer Control
Language (PCL) or PostScript (if printing to the destination printer).

# Configuring and Managing Print Services

Red Hat's print system can be used to print to local (attached) or remote (network) printers. If you use a local printer, it is represented by a printer device, such as /dev/lpd0 or /dev/usb/lpd0 (if you have a USB printer). Local and remote printer definitions, known as print queues, are contained in your system's printer capabilities database, /etc/printcap. Each printer listed in this database will have a corresponding print queue spool, under /var/ spool/lpd with the printer's queue name. A document being printed is known as a print job, and you can view a list of, queue, or current print jobs in the spool directory.

To add a printer to your Red Hat Linux system, use the redhat-config-printer client to create, configure, and define the printer. The client saves the definition as an entry in your system's printer capabilities database, /etc/printcap. Each definition contains a text field that points to related and appropriately named spool directory under /var/ spool/lpd. This spool directory will hold copies of printed documents to await printing.

Along with the spool directory, the printer's printcap listing contains an entries that points to /usr/share/printconf/util/mf/wrapper. This file is a script that calls the /usr/bin/magicfilter-t utility.

A sample printer description with an if: filter entry (the shell script pointer that calls the utility) looks like this:

```
lpd:
:ml0:\
:mx#:\
:sd=/var/sp/lpd/lp:\n:af=/var/sp/lpd/lp/lpd.acct:\n:sh:
:lp=/dev/lpd0:
:lpd_bounce=true:\n:if=/usr/share/printconf/util/mf_wrapper:
```

In this example, the mf_wrapper filter utility is used as a printer filter, used to transform the printed document into an acceptable form when mf_wrapper calls a related utility (magicfilter-t) to identify the file stream as a text file, document, or image, according to initial-byte headers, or magic values, as listed in the file /usr/share/printconf/mf.magic.

> NOTE
These magic values are contained in the first bytes of many documents. They are used by the file command, which can display a file's type even if the filename is an extension. For example, PostScript documents normally have a filename extension of .ps. However, if the extension is missing, the document's format may not be readily apparent. The file command can be used to determine one or more file types like so:

# Configuring and Managing Print Services

$ file tiger art_collection
tiger: PostScript document text conforming to level 2.0 - type EPS
art_collection: Zip archive data, at least v2.0 to extract

In this example, the file named tiger is a PostScript document, whereas the file named art-collection is a compressed archive.

The magicfilter-t utility then governs the stream to PostScript, using filter rules located
at the /usr/share/printconf/mf_rules directory.
The values returned by these filter rules assign proper arguments to the Ghostscript
PostScript interpreter, gs, according to the type of destination printer. The interpreter
reads the input file as PostScript and then converts the stream to the format or
language understood by the destination printer. The data stream, using Printer Control
Language (PCL) or PostScript (if printing to the destination printer).

# Configuring and Managing Print Services

Red Hat's print system can be used to print to local (attached) or remote (network) printers. If you use a local printer, it is represented by a printer device, such as /dev/lpd0 or /dev/usb/lpd0 (if you have a USB printer). Local and remote printer definitions, known as print queues, are contained in your system's printer capabilities database, /etc/printcap. Each printer listed in this database will have a corresponding print queue spool, under /var/ spool/lpd with the printer's queue name. A document being printed is known as a print job, and you can view a list of, queue, or current print jobs in the spool directory.

To add a printer to your Red Hat Linux system, use the redhat-config-printer client to create, configure, and define the printer. The client saves the definition as an entry in your system's printer capabilities database, /etc/printcap. Each definition contains a text field that points to related and appropriately named spool directory under /var/ spool/lpd. This spool directory will hold copies of printed documents to await printing.

Along with the spool directory, the printer's printcap listing contains an entries that points to /usr/share/printconf/util/mf/wrapper. This file is a script that calls the /usr/bin/magicfilter-t utility.

A sample printer description with an if: filter entry (the shell script pointer that calls the utility) looks like this:

```
lpd:
:ml0:\
:mx#:\
:sd=/var/sp/lpd/lp:\n:af=/var/sp/lpd/lp/lpd.acct:\n:sh:
:lp=/dev/lpd0:
:lpd_bounce=true:\n:if=/usr/share/printconf/util/mf_wrapper:
```

In this example, the mf_wrapper filter utility is used as a printer filter, used to transform the printed document into an acceptable form when mf_wrapper calls a related utility (magicfilter-t) to identify the file stream as a text file, document, or image, according to initial-byte headers, or magic values, as listed in the file /usr/share/printconf/mf.magic.

> NOTE
These magic values are contained in the first bytes of many documents. They are used by the file command, which can display a file's type even if the filename is an extension. For example, PostScript documents normally have a filename extension of .ps. However, if the extension is missing, the document's format may not be readily apparent. The file command can be used to determine one or more file types like so:

# Configuring and Managing Print Services

$ file tiger art_collection
tiger: PostScript document text conforming to level 2.0 - type EPS
art_collection: Zip archive data, at least v2.0 to extract

In this example, the file named tiger is a PostScript document, whereas the file named art-collection is a compressed archive.

The magicfilter-t utility then governs the stream to PostScript, using filter rules located
at the /usr/share/printconf/mf_rules directory.
The values returned by these filter rules assign proper arguments to the Ghostscript
PostScript interpreter, gs, according to the type of destination printer. The interpreter
reads the input file as PostScript and then converts the stream to the format or
language understood by the destination printer. The data stream, using Printer Control
Language (PCL) or PostScript (if printing to the destination printer).

# Configuring and Managing Print Services

Red Hat's print system can be used to print to local (attached) or remote (network) printers. If you use a local printer, it is represented by a printer device, such as /dev/lpd0 or /dev/usb/lpd0 (if you have a USB printer). Local and remote printer definitions, known as print queues, are contained in your system's printer capabilities database, /etc/printcap. Each printer listed in this database will have a corresponding print queue spool, under /var/ spool/lpd with the printer's queue name. A document being printed is known as a print job, and you can view a list of, queue, or current print jobs in the spool directory.

To add a printer to your Red Hat Linux system, use the redhat-config-printer client to create, configure, and define the printer. The client saves the definition as an entry in your system's printer capabilities database, /etc/printcap. Each definition contains a text field that points to related and appropriately named spool directory under /var/ spool/lpd. This spool directory will hold copies of printed documents to await printing.

Along with the spool directory, the printer's printcap listing contains an entries that points to /usr/share/printconf/util/mf/wrapper. This file is a script that calls the /usr/bin/magicfilter-t utility.

A sample printer description with an if: filter entry (the shell script pointer that calls the utility) looks like this:

```
lpd:
:ml0:\
:mx#:\
:sd=/var/sp/lpd/lp:\n:af=/var/sp/lpd/lp/lpd.acct:\n:sh:
:lp=/dev/lpd0:
:lpd_bounce=true:\n:if=/usr/share/printconf/util/mf_wrapper:
```

In this example, the mf_wrapper filter utility is used as a printer filter, used to transform the printed document into an acceptable form when mf_wrapper calls a related utility (magicfilter-t) to identify the file stream as a text file, document, or image, according to initial-byte headers, or magic values, as listed in the file /usr/share/printconf/mf.magic.

> NOTE
These magic values are contained in the first bytes of many documents. They are used by the file command, which can display a file's type even if the filename is an extension. For example, PostScript documents normally have a filename extension of .ps. However, if the extension is missing, the document's format may not be readily apparent. The file command can be used to determine one or more file types like so:

# Configuring and Managing Print Services

$ file tiger art_collection
tiger: PostScript document text conforming to level 2.0 - type EPS
art_collection: Zip archive data, at least v2.0 to extract

In this example, the file named tiger is a PostScript document, whereas the file named art-collection is a compressed archive.

# GUI-Based Printer Configuration Quickstart

- Overview of Red Hat Linux Printing
- Configuring and Managing Print Services
- Creating and Configuring Local Printers
- Creating Network Printers
- Console Print Control
- Using the Common Unix Printing System (CUPS)
- Avoiding Printer-Support Problems
- Reference

> NOTE Hat's print system can be used to print to local (attached) or remote (network) printers. If you use a local printer, it is represented by a printer device, such as /dev/lpd0 or /dev/usb/lpd0 (if you have a USB printer). Local and remote printer definitions, known as print queues, are contained in your system's printer capabilities database, /etc/printcap. Each printer listed in this database will have a corresponding print queue spool, under /var/ spool/lpd with the printer's queue name. A document being printed is known as a print job, and you can view a list of, queue, or current print jobs in the spool directory.

To add a printer to your Red Hat Linux system, use the redhat-config-printer client to create, configure, and define the printer. The client saves the definition as an entry in your system's printer capabilities database, /etc/printcap. Each definition contains a text field that points to related and appropriately named spool directory under /var/ spool/lpd. This spool directory will hold copies of printed documents to await printing.

Along with the spool directory, the printer's printcap listing contains an entries that points to /usr/share/printconf/util/mf/wrapper. This file is a script that calls the /usr/bin/magicfilter-t utility.

A sample printer description with an if: filter entry (the shell script pointer that calls the utility) looks like this:

```
lpd:
:ml0:\
:mx#:\
:sd=/var/sp/lpd/lp:\n:af=/var/sp/lpd/lp/lpd.acct:\n:sh:
:lp=/dev/lpd0:
:lpd_bounce=true:\n:if=/usr/share/printconf/util/mf_wrapper:
```

In this example, the mf_wrapper filter utility is used as a printer filter, used to transform the printed document into an acceptable form when mf_wrapper calls a related utility (magicfilter-t) to identify the file stream as a text file, document, or image, according to initial-byte headers, or magic values, as listed in the file /usr/share/printconf/mf.magic.

> NOTE
These magic values are contained in the first bytes of many documents. They are used by the file command, which can display a file's type even if the filename is an extension. For example, PostScript documents normally have a filename extension of .ps. However, if the extension is missing, the document's format may not be readily apparent. The file command can be used to determine one or more file types like so:

# Configuring and Managing Print Services

$ file tiger art_collection
tiger: PostScript document text conforming to level 2.0 - type EPS
art_collection: Zip archive data, at least v2.0 to extract

In this example, the file named tiger is a PostScript document, whereas the file named art-collection is a compressed archive.

The magicfilter-t utility then governs the stream to PostScript, using filter rules located
at the /usr/share/printconf/mf_rules directory.
The values returned by these filter rules assign proper arguments to the Ghostscript
PostScript interpreter, gs, according to the type of destination printer. The interpreter
reads the input file as PostScript and then converts the stream to the format or
language understood by the destination printer. The data stream, using Printer Control
Language (PCL) or PostScript (if printing to the destination printer).

# GUI-Based Printer Configuration Quickstart

Configuring a printer for Red Hat is easy but must be done using root permission. If you're using Red Hat's desktop, select the Printing menu from the System Settings. You will be asked to enter the root password. If not, you're using X as root, which is a bad idea. Log out, and then log in as a regular user.
