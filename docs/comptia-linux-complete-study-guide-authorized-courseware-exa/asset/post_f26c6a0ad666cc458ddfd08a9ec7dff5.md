
## Squeezing Ghostscript into the Queue

Printing to a non-PostScript printer in Linux requires fitting Ghostscript into the print queue. This is generally done through the use of a *smart filter*. This is a program that’s called as part of the printing process. The smart filter examines the file that’s being printed, determines its type, and passes the file through one or more additional programs before the printing software sends it on to the printer. The smart filter can be configured to call Ghostscript with whatever parameters are appropriate to produce output for the queue’s printer.

CUPS ships with its own set of smart filters, which it calls automatically when you tell the system what model printer you’re using. CUPS provides a Web-based configuration tool, as described in the upcoming section “Using the Web-Based CUPS Utilities.” This system, or distribution-specific GUI printer configuration tools, can make setting up a printer for CUPS fairly straightforward.

The end result of a typical Linux printer queue configuration is the ability to treat any supported printer as if it were a PostScript printer. Applications that produce PostScript output can print directly to the queue. The smart filter detects that the output is PostScript and runs it through Ghostscript. The smart filter can also detect other file types, such as plain text and various graphics files, and it can send them through appropriate programs instead of or in addition to Ghostscript in order to create a reasonable printout.

If you have a printer that can process PostScript, the smart filter is usually still involved, but it doesn’t pass PostScript through Ghostscript. In this case, the smart filter passes PostScript directly to the printer, but it still sends other file types through whatever processing is necessary to turn them into PostScript.

## Running a Printing System

Because Linux printing systems run as daemons, they must be started before they’re useful. This task is normally handled automatically via startup scripts in /etc/rc.d, /etc/init.d, or /etc/rc?.d (where ? is a runlevel number). Look for startup scripts that contain the string `cups` (or `lpd` or `lprng` for older systems) in their names to learn what your system is running. If you’re unsure if a printing system is currently active, use the `ps` utility to search for running processes by these names, as in:

```bash
$ ps ax | grep cups
1896 ? 5s 0:01 cupsd
```

This example shows that `cupsd`, the CUPS daemon, is running, so the system is using CUPS for printing. If you can’t find any running printing system, consult your distribution’s documentation to learn what is available and check that the appropriate package is installed. All major distributions include startup scripts that should start the appropriate printing daemon when the computer boots.

## Configuring CUPS

CUPS uses various configuration files in the `/etc/cups` directory and its subdirectories to manage its operation. You can edit these files directly, and you may need to do so if you want to share printers or use printers shared by other CUPS systems. The simplest way to add printers to CUPS, though, is to use the tool's Web-based configuration utility.

### Editing the CUPS Configuration Files

You can add or delete printers by editing the `/etc/cups/printers.conf` file, which consists of printer definitions. Each definition begins with the name of a printer, identified by the string `DefaultPrinter` (for the default printer) or `Printer` (for a nondefault printer) in angle brackets (`<>`), as in the following:

```
<DefaultPrinter okidata>
```

This line marks the beginning of a definition for a printer queue called `okidata`. The end of this definition is a line that reads `</Printer>`. Intervening lines set assorted printer options, such as identifying string, the printer's location (its local hardware port or network location), its current status, and so on. Additional options are stored in a PostScript Printer Definition (PPD) file that's named after the queue and stored in the `/etc/cups/ppd` subdirectory. PPD files follow an industry-standard format. For PostScript printers, you can obtain a PPD file from the printer manufacturer, typically from a driver CD-ROM or from the manufacturer's Web site. CUPS and its add-on driver packs also ship with a large number of PPD files that are installed automatically when you use the Web-based configuration utilities.

As a general rule, you're better off using the CUPS Web-based configuration tools to add printers rather than adding printers by directly editing the configuration files. If you like, though, you can study the underlying files and tweak the configurations using a text editor to avoid having to go through the full Web-based tool to make a minor change.

One exception to this rule relates to configuring the CUPS Web-based interface tool itself and CUPS' ability to interface with other CUPS systems. One of the great advantages of CUPS is that it uses a new network printing protocol, known as the Internet Printing Protocol (IPP), in addition to the older LPD protocol used by BSD LPD and LPRng. IPP supports a feature it calls browsing, which enables computers on a network to automatically exchange printer lists. This feature can greatly simplify configuring network printing. You may need to change some settings in the main CUPS configuration file, `/etc/cups/cupsd.conf`, to enable this support.

The `/etc/cups/cupsd.conf` file, which is structurally similar to the Apache Web server configuration file, contains a number of configuration blocks that specify which other systems should be able to access it. Each block controls access to a particular location on the server. These blocks look like this:

```
<Location /printers>
Order Deny,Allow
Deny from All
BrowseAllow from 127.0.0.1
BrowseAllow from 192.168.1.0/24
BrowseAllow from @LOCAL
Allow from 127.0.0.1
Allow from 192.168.1.0/24
Allow from @LOCAL
</Location>
```

![](img/f339a9f48c4b443e61c74acb4c9c3da4_369_0.png)

If you’re configuring a workstation with a local printer that you don’t want to share, or if you want to configure a workstation to use printers shared via LPD or some other non-IPP printing protocol, you shouldn’t need to adjust `/etc/cups/cupsd.conf`. If you want to access remote IPP printers, however, you should at least activate browsing by setting the directive `Browsing On`, as described shortly. You shouldn’t have to modify your location definitions unless you want to share your local printers.

The `/printers` location, shown here, controls access to the printers themselves. The following list includes features of this example:

- **Directive order**: The `Order Deny, Allow` tells CUPS in which order it should apply allow and deny directives—in this case, allow directives modify deny directives.
- **Default policy**: The `Deny from All` line tells the system to refuse all connections except those that are explicitly permitted.
- **Browsing control lines**: The `BrowseAllow` lines tell CUPS from which other systems it should accept browsing requests. In this case, it accepts connections from itself (`127.0.0.1`), from systems on the `192.168.1.0/24` network, and from systems connected to local subnets (`@LOCAL`).
- **Access control lines**: The `Allow` lines give the specified systems non-browse access to printers—that is, those systems can print to local printers. In most cases, the `Allow` lines are the same as the `BrowseAllow` lines.

You can also create a definition that uses `Allow from All` and then creates `BrowserDeny` and `Deny` lines to limit access. As a general rule, though, the approach shown in this example is safer. Locations other than the `/printers` location can also be important. For instance, there’s a root (`/`) location that specifies default access permissions to all other locations and an `/admin` location that controls access to CUPS administrative functions.

Before the location definitions in `cupsd.conf` are a few parameters that enable or disable browsing and other network operations. You should look for the following options specifically:

- **Enabling browsing**: The `Browsing` directive accepts `On` and `Off` values. The CUPS default is to enable browsing (`Browsing On`), but some Linux distributions disable it by default.
- **Browsing access control**: The `BrowseAddress` directive specifies the broadcast address to which browsing information should be sent. For instance, to broadcast data on your printers to the `192.168.1.0/24` subnet, you’d specify `BrowseAddress 192.168.1.255`.
