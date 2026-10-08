![](bbox=[0.05, 0.11, 0.13, 0.18])

# file - Run test to classify file.

file(1)
file(1)
NAME
file - determine file type
SYNOPSIS
file [-m mfile] [-c] [-f ffile] file ...
DESCRIPTION
file performs a series of tests on each file in an attempt to classify it. If file appears to be an ASCII file, file examines the first 512 bytes and tries to guess its language. If file is an executable a.out file, file prints the version stamp, provided it is greater than 0 (see the description of the -V option in ld(1)).
file uses the file /etc/magic to identify files that have some sort of magic number, that is, any file containing a numeric or string constant that indicates its type. Commentary at the beginning of /etc/magic explains the format.

Options
file recognizes the following command-line options:
-m mfile
use alternate magic file mfile.
-c
Check the magic file for format errors. This validation is not normally carried out for reasons of efficiency. No file classification is done when this option is specified.
-f ffile
Obtain the list of files to be examined from file ffile. file classifies each file whose name appears in ffile.

EXTERNAL INFLUENCES
Environment Variables
LC_MESSAGES determines the language in which messages are displayed.
If LC_MESSAGES is not specified in the environment or is set to the empty string, the value of LANG is used as a default for each unspecified or empty variable. If LANG is not specified or is set to the empty string, a default of "C" (see lang(5)) is used instead of LANG.
If any internationalization variable contains an invalid setting, file behaves as if all internationalization variables are set to "C". See environ(5).

International Code Set Support
Single- and multi-byte character code sets are supported. However, all non-ASCII text files are identified as "data".