| -o *file* | Send output to *file*. If *file* is specified as "-", use standard output. |
| -P *printer* | Use *printer*. If a printer is not specified, the system default printer is used. |
| -R | Portrait orientation. |
| -r | Landscape orientation. |
| -T *number* | Set tab stops to every *number* characters. |
| -u *text* | Underlay (watermark) pages with *text*. |

This is just a summary. a2ps has several more options.

Note: a2ps is still in active development. During my testing, I noticed different behavior on various distributions. On CentOS 4, output always went to standard output by default. On CentOS 4 and Fedora 10, output defaulted to A4 media, despite the program being configured to use letter-size media by default. I could overcome these issues by explicitly specifying the desired option. On Ubuntu 8.04, a2ps performed as documented.

Also note that there is another output formatter that is useful for converting text into PostScript. Called ensript, it can perform many of the same kinds of formatting and printing tricks, but unlike a2ps, it only accepts text input.

# Monitoring And Controlling Print Jobs

As Unix printing systems are designed to handle multiple print jobs from multiple users, CUPS is designed to do the same. Each printer is given a print queue, where jobs are parked until they can be spooled to the printer. CUPS supplies several command line programs that are used to manage printer status and print queues. Like the lpr and lp programs, these management programs are modeled after the corresponding programs from the Berkeley and System V printing systems.

# lpstat – Display Print System Status

The lpstat program is useful for determining the names and availability of printers on the system. For example, if we had a system with both a physical printer (named “printer”) and a PDF virtual printer (named “PDF”), we could check their status like this: