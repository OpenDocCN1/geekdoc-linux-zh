# ADAPTATION OF INDIVIDUAL PROGRAMS 257

# 9.7.1 The program less

The program less can display foreign language characters if the appropriate locale files are installed and activated. Older versions of less are used to evaluate the environment variable LESSCHARSET, others the value ISO-8859-1 in the variable LC_CTYPE.

| Additional Information and Sources |
|---||
| Man pages: less(1), lesskey(1) |
| Newsgroups: gnu.utils.bug |
| Package: less-257.tar.gz |
| ftp server: ftp.gnu.org |
| ftp path: /pub/gnu |
| Size: about 150 Kbytes |

# 9.7.2 The program package groff

The groff is a text formatter that can translate texts in nroff or troff format into a series of output formats. If you want to convert the text into a directly readable format, you must not select ascii as your output device, or latin1 (with the command line option -T latin1) to show foreign language characters in the output.

The formatting system includes a number of programs, for example gtbl for setting tables or qeqn for setting formulae. Here, too, the output device must be selected correspondingly.

# A4 paper format

If you need to use A4 paper format (297 mm by 210 mm), you must set the environment variable PAGE to the value A4 before starting the configure script.

If the configuration file /usr/lib/groff/font/devps/DESC contains the line ^length 841890, groff outputs in PostScript format on A4 paper. The same entry can be included in the file /usr/lib/groff/font/devdvi if the DVI² output is also to be formatted for A4 paper.

The setting of paper formats is not defined by standards, therefore manual intervention is required. This also applies to a number of other programs.

DVI = Device Independent