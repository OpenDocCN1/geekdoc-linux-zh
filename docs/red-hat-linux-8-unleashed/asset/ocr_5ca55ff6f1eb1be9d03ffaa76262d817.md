# Configuring and Managing Print Services

$ file tiger art_collection
tiger: PostScript document text conforming to level 2.0 - type EPS
art_collection: Zip archive data, at least v2.0 to extract

In this example, the file named tiger is a PostScript document, whereas the file named art-
collection is a compressed archive.

The magicfilter-t utility then governs the stream to PostScript, using filter rules located
at the /usr/share/printconf/mf_rules directory.
The values returned by these filter rules assign proper arguments to the Ghostscript
PostScript interpreter, gs, according to the type of destination printer. The interpreter
reads the input file as PostScript and then converts the stream to the format or
language understood by the destination printer. The data stream, using Printer Control
Language (PCL) or PostScript (if printing to a PostScript printer) is then to set the desired
printer.

# Configuring and Managing Print Services

Your task as a system administrator (root operator of your workstation) is to properly
define entries in /etc/printcap for local or remote printers and to ensure that printing
services are enabled and running properly. Fortunately, Red Hat's graphical service
configuration tools make this job easy, and you should use Red Hat's tools to configure
printing. How you learn in this section of the chapter. But first, take a moment to read
through a quick overview of the configuration process.

> CAUTION
Do not manually edit your Red Hat /etc/printcap. Changes will be lost when printing
service is restarted, or if your system is rebooted. If you need to create customized print entries,
s the entries in /etc/printcap.local and then restart print service.

You can configure Red Hat Linux services using either the command line redhat-
config-printer ui program or the redhat-config-printer ui graphical interface. Most
of the detailed information in this chapter refers to the use of the GUI. The overview
se that follow, however, give you solid foundation in both configuration approaches.
Learn the details of these processes in later sections of the chapter.

# GUI-Based Printer Configuration Quickstart

Configuring a printer for Red Hat Linux is easy but must be done using root permission.
Make sure that the lpd printer daemon is installed and running. If you elect to use print-
support when you install Red Hat, the daemon and related software will be installed.
lpd is installed but not running, start the daemon like so:

```
# /etc/rc.d/init.d/ldp start
```