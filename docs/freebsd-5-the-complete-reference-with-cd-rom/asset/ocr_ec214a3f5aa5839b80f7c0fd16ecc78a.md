The /etc/printcap file supports a large number of options. To understand them, first consider a sample entry for a single printer, as shown in Listing 9-1. (If your system can print to multiple printers, or uses one printer in multiple ways, you may have several such entries.)

> **Listing 9-1**
> Sample
> /etc/
> printcap
> Entry
> lp/hp4000:\
>   :lp=/dev/lpt0:\
>   :br#115200:\
>   :sd=/var/spool/lpd/hp4000:\
>   :mx#0:\
>   :sh:

Each entry begins with one or more names for the printer. Many applications use a default printer name of lp, so this entry includes this name as the printer's first name. (If your system supports multiple printers, only one should have the lp name.) If you use multiple names, separate them from one another with a vertical bar (|); in this case, the printer can be accessed as both lp and hp4000 with identical results.

The /etc/printcap file format specifies that each printer definition occupy one line, with colons (:) separating entries. To improve readability, though, most implementations use the common practice of using a backslash (\) as a line continuation character. Note that in Listing 9-1, every line except for the last one ends in a backslash. The second and subsequent lines of each entry are also indented, to make it easier to spot where one entry ends and another begins.

Most options are short codes, often followed by an equal sign (=) or a pound sign (#) to set the option's value. The printcap man page includes descriptions of these options. The most common are

+   - lp This option sets the printer device file, such as /dev/lpt0 or /dev/lpt1. You should omit this option if you're configuring a network printer (that is, a printer that's connected to another computer or that has a direct network connection; if you intend to share a printer that's connected via a parallel, RS-232 serial, or USB port, you must still make this entry).

+   - br This option sets the baud rate for RS-232 printers. In the case of Listing 9-1, it's not a necessary entry because the printer device is a parallel printer. Thus, it could be omitted from Listing 9-1. Leaving the entry in place does no harm, though. Normally, you should set this value as high as you can. Listing 9-1's 115200 works well in most cases, but sometimes you may need to reduce this to 57600 or lower.

+   - rm This option is used only on network printers. It's the name of the remote print server, such as rm=gutenberg.threeroomco.com. This option must be absent when you're configuring a printer that's attached to a local port.

+   - rp This option is used in conjunction with rm to set the name of the print queue on a remote system. For instance, if the remote system called its printer wgprint, you'd set this value as rp=wgprint. Confusion is reduced if you use