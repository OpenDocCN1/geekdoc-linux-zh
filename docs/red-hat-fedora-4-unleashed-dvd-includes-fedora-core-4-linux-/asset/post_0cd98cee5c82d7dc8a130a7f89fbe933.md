
## Graphics

- eog—Eye of Gnome image viewer
- ImageMagick—An image manipulation application
- gimp—The GNU Image Manipulation Program
- gqview—GNOME image viewer
- kcoloredit—KDE palette editor
- kiconedit—KDE icon editor
- kpaint—A graphics application
- kquickshow—KDE image-viewing application
- kview—KDE embedded image viewer.
- netpbm-progs—Tools for manipulating netpbm-formatted graphics
- xfig—A vector graphic application

## Reference

- http://www.cdcopyworld.com/—A resource for technical information about CD media and CD writers.
- http://hardware.redhat.com/hcl/—A database of supported hardware.
- http://www.opensound.com/download.cgi—The commercial OSS sound driver trial version download.
- http://www.xmms.org/—Home to the Xmms audio player.
- http://www.thekompany.com/projects/tcogripper/—A free (but not GPL) OGG CD ripper.
- http://faceprint.com/code/—An MP3 to OGG converter named mp32ogg.
- http://www.ibiblio.org/pub/linux/apps/sound/convert/INDEX.html—Home to several sound conversion utilities.
- http://linux-sound.org/—An excellent resource for Linux music and sound.
- http://www.cnpbagwell.com/audio.html—The Audio Format FAQ.
- http://www.iccast.org/—A streaming audio server.
- http://www.linuxnetmag.com/en/issue4/m4icecast1.html—An Icecast tutorial.
- http://linuxselfhelp.com/HOWTO/MP3-HOWTO-7.html—The MP3 HOWTO contains brief descriptions of many audio applications and, although it focuses on the MP3 format, the information is easily generalized to other music formats.
- http://www.exploits.org/v4/—Video for Linux resources.
- http://fame.sourceforge.net/—Video encoding tools.
- http://teletext.mb21.co.uk/faq.shtml—The Teletext FAQ.
- http://xine.sourceforge.net/—Home of the Xine DVD/video player.
- http://www.MPlayerHQ.hu/homepage/—Home to the MPlayer video player.
- http://www.videolan.org/—A VideoLAN project with good documentation.
- http://fy.chalmers.se/~appro/linux/DVD+RW/—The DVD+RW/+R-R[W] for Linux, a HOWTO for creating DVDs under Linux.

## Printing with Fedora

### IN THIS CHAPTER

- Overview of Fedora Printing
- Configuring and Managing Print Services
- Creating and Configuring Local Printers
- Reference

Fedora supports more than 600 printers from more than 40 manufacturers, and it is possible to mix and match printing hardware with newer computers. In this chapter, you learn about printing services offered in Fedora. Here, you also learn about the many different programs, files, and directories that are integral to supporting printing under Fedora. The chapter also shows you simple techniques for configuring new printers. You learn a variety of methods for making printers available for use quickly and easily, and you learn some important workarounds for connecting printer and system hardware with differing port configurations.

Fedora uses the Common Unix Printing System (CUPS). Other printing systems, such as LPRng, can be used as the printing system, but you might not be able to use some of the graphical print management utilities included with Fedora. For information on avoiding printer headaches refer to “Avoiding Printer-Support Problems” in Chapter 21, “File and Print.”

### The Internet Printing Protocol

CUPS supports the Internet Printing Protocol, known as IPP, and offers a number of unique features, such as network printer directory (printer browsing) services, support for encryption, and support for PostScript Printer Description (.ppd) files.

According to the Internet Engineering Task Force (IETF), IPP grew out of a 1996 proposal by Novell to create a printing protocol for use over the Internet. Since then, the system has been developed and has matured into a stable print system for use on a variety of Linux and Unix-like operating platforms.

### Overview of Fedora Printing

Fedora's print filter system is the main engine that enables the printing of many types of documents. The heart of that engine is the GNU GPL version of Aladdin's Ghostscript interpreter, the gs client. The system administrator's printer configuration tool is the system-config-printer client.

> NOTE: Fedora's print system can be used to print to local (attached) or remote (network) printers. If you use a local printer, it is represented by a printer device, such as /dev/lp0 or /dev/usb/lp0 (if you have a USB printer). Local and remote printers use print queues defined in your system's printer capabilities database, /etc/printcap. A document being printed is known as a print job, and you can view and control your list, or queue, of current print jobs in the spool directory, which is /var/spool/cups. Note that you may only manage your print jobs; only the root operator can control print jobs of any user on the system.

To add a printer to your system, you use the system-config-printer client to create, configure, and save the printer's definition. The client saves the definition as an entry in your system's printer capabilities database, /etc/printcap. Each definition contains a text field with the name of the printer, its host, and name of the print queue. Printed documents will be spooled to the /var/spool/cups directory. A sample printcap definition might look like:

```
# This file was automatically generated by cupsd(8) from the
# /etc/cups/printers.conf file. All changes to this file
# will be lost.
lp|lp:rm=stinky:rp=lp:
```

CUPS maintains its own database of defined printers under the /etc/cups directory in a file named printers.conf. For example, an associated printer defined in /etc/printcap previously might have the following entry in /etc/cups/printers.conf:

```
<DefaultPrinter lp>
Info Created by redhat-config-printer 0.6.x
DeviceURI parallel:/dev/lp0
Location HP 648 local printer
State Idle
Accepting Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
</Printer>
```

This example shows the definition for the printer named `lp`, along with its associated device, description, state, and other information. The various possible fields and entries in this file are documented in the `printer.conf` man page.

CUPS uses a print server (daemon) named `cupsd`, also called a *scheduler* in the CUPS documentation. The server can be controlled, like other Fedora services, by the `service` command or `system-config-services` client. How the server works on a system is determined by settings in its configuration file, `cupsd.conf`, found under the `/etc/cups` directory. CUPS executables are found under the `/usr/lib/cups` directory.

The `cupsd.conf` man page documents more than 80 different settings for the server, which you can configure to match your system, network, or printing environment. Default CUPS-related files and directories are stored under the `/usr/share/cups` directory. Logging can be set to seven different levels, with information about access and errors stored in log files under the `/var/log/cups` directory.

Resource requirements can be tailored through other settings, such as `MaxCopies` to set the maximum number of copies of a print job by a user, `MaxJobs` to set a limit on the number of active print jobs, and `MaxJobsPerUser` to set a limit on the number of active jobs per user. The `RICache` setting (8MB by default) controls the amount of memory used for graphics cache during printing.

For example, if you want to limit printing to 20 copies of a document or page at a time and only 10 simultaneous print jobs per user, use settings such as:

```
MaxCopies 20
MaxJobsPerUser 10
```

> **TIP**: Don’t forget to restart the CUPS server after making any changes to its configuration file. Changes are only activated when the service is restarted (when the daemon rereads its configuration file). See the section “GUI-Based Printer Configuration Quickstart” later on.

Because CUPS does not use the traditional Berkeley-style print spooling system, `lpd`, you can change the name of the printer capabilities database from the default `/etc/printcap`. Encryption can be used for printing, with secure access behavior determined by settings in `/etc/cups/client.conf`. Network access settings include port, connection, IP address, domains, and limits to the number and size of client requests.

### Configuring and Managing Print Services

Your task as a system administrator (or root operator of your workstation) is to properly define local or remote printers and to ensure that printing services are enabled and running properly. Fortunately, Fedora includes Red Hat’s graphical print service configuration tools that make this job easy. You should use these tools to configure printing, as you learn in this section of the chapter. But first, take a moment to read through a quick overview of the configuration process.
