# PRINTING UNDER LINUX 119

A single entry (capability) consists of a two-character code. These codes are described in the man page printcap(5). Codes that need a parameter are followed by an equals sign (=), whereas numeric parameters are separated by a hash sign (#).

+   - The first field specifies the name of the printer. Several alternative names for the same printer are separated by vertical bars (|). The last name is usually the longest.

+   - The value lp (line printer) specifies the interface to be used for printing. Here, a local interface is used.

+   - The value sd (spool directory) defines the directory in which print jobs are buffered. A separate directory should be used for each.

+   - The value sh (suppress header) suppresses the printing of the header page. This is sensible for single-user systems, whereas printers used by several users should at least print a brief header line (sb = short banner). If a printer is used by a large number of users, printing a separation page between the listings is a good idea.

+   - By default, the printing system accepts only jobs that are smaller than 1 Mbyte. The size limit can be changed by setting mx to a different value, where 0 stands for unlimited size. Another possibility for printing large files is to use the -s option when printing with lpr. You must neither modify delete a file until it has completely finished printing.

+   - The value l0 specifies the name to be used for the lock file.

+   - The file /var/log/lpd is used as a log file. The name is determined by the capability lf.

Many (different) printers can be included in the /etc/printcap file. A system default printer is usually called lp. By means of the environment variable PR each user can set another printer as the default. Furthermore, another printer can be selected when calling lpr with the -P option. Detailed information on the printing system and its configuration can be found in the manual pages of lpr(1), lpq(1), lrpm(1), lpd(8), lpc(8), and printcap(5), and in the Printing How.

Printing on remote computers The lpr system also provides the ability to print on remote computers. Obviously, a network connection must exist between these computers. More on the subject of networks can be found in Chapter 14.