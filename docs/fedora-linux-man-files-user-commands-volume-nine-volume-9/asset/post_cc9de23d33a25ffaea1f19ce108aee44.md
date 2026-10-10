
## Iconv Issues

`preconv` by itself only supports three encodings: latin-1, cp1047, and UTF-8; all other encodings are passed to the `iconv` library functions. At compile time it is searched and checked for a valid `iconv` implementation; a call to `preconv --version` shows whether `iconv` is used.

The only relevant tag for **preconv** is `coding` which can take the values listed below. Here an example line which tells **Emacs** to edit a file in troff mode, and to use latin2 as its encoding.

```text
." -*- mode: troff; coding: latin-2 -*-
```

The following list gives all MIME coding tags (either lowercase or uppercase) supported by **preconv**; this list is hard-coded in the source.

- big5, cp1047, euc-jp, euc-kr, gb2312, iso-8859-1, iso-8859-2, iso-8859-5, iso-8859-7, iso-8859-9, iso-8859-13, iso-8859-15, koi8-r, us-ascii, utf-8, utf-16, utf-16be, utf-16le

In addition, the following hard-coded list of other tags is recognized which eventually map to values from the list above.

- ascii, chinese-big5, chinese-euc, chinese-iso-8bit, cn-big5, cn-gb, cn-gb-2312, cp878, csascii, csisolatin1, cyrillic-iso-8bit, cyrillic-koi8, euc-china, euc-cn, euc-japan, euc-japan-1990, euc-korea, greek-iso-8bit, iso-10646/utf8, iso-10646/utf-8, iso-latin-1, iso-latin-2, iso-latin-5, iso-latin-7, iso-latin-9, japanese-euc, japanese-iso-8bit, jis8, koi8, korean-euc, korean-iso-8bit, latin-0, latin1, latin-1, latin-2, latin-5, latin-7, latin-9, le-utf-8, le-utf-16, le-utf-16be, le-utf-16-le, le-utf-16be-with-signature, le-utf-16le, le-utf-16-le, le-utf-16le-with-signature, utf8, utf-16-be, utf-16-be-with-signature, utf-16be-with-signature, utf-16-le, utf-16-le-with-signature, utf-16le-with-signature

Those tags are taken from **GNU Emacs** and **XEmacs**, together with so aliases. Trailing `-dos`, `-unix`, and `-mac` suffixes of coding tags (which give the end-of-line convention used in the file) are stripped off before the comparison with the above tags happens.

### BUGS

**preconv** doesn't support *local variable lists* yet. This is a different syntax form to specify local variables at the end of a file.

### SEE ALSO

(1) the **GNU Emacs** and **XEmacs** info pages

### COPYING

Copyright 2006-2014 Free Software Foundation, Inc.

Permission is granted to make and distribute verbatim copies of this manual provided the copyright notice and this permission notice are preserved on all copies.

Permission is granted to copy and distribute modified versions of this manual under the conditions for verbatim copying, provided that the entire resulting derived work is distributed under the terms of a permission notice identical to this one.

Permission is granted to copy and distribute translations of this manual into another language, under the above conditions for modified versions, except that this permission notice may be included in translations approved by the Free Software Foundation instead of in the original English.

## PRINTAFM

### NAME

printafm - Print the trics from a Postscript font in AFM format using ghostscript

### SYNOPSIS

```text
printafm fontna
```

### DESCRIPTION

This script invokes (1) to print the trics from a font in AFM format. Output goes to stdout.

### SEE ALSO

(1)

### VERSION

This document was last revised for Ghostscript version 9.16.

### AUTHOR

Artifex Software, Inc. are the primary maintainers of Ghostscript. This manpage by George Ferguson.

## PRINTENV

### NAME

printenv - print all or part of environment

### SYNOPSIS

```text
printenv [OPTION]... [VARIABLE]...
```

### DESCRIPTION

Print the values of the specified environment VARIABLE(s). If no VARIABLE is specified, print name and value pairs for them all.

- -0, --null
  end each output line with NUL, not newline

- --help
  display this help and exit

- --version
  output version information and exit

NOTE: your shell may have its own version of printenv, which usually supersedes the version described here. Please refer to your shell's documentation for details about the options it supports.

### AUTHOR

Written by David MacKenzie and Richard Mlynarik.

### REPORTING BUGS

GNU coreutils online help: <http://www.gnu.org/software/coreutils/> Report printenv translation bugs to <http://translationproject.org/report.html>

### COPYRIGHT

Copyright 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>. This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

### SEE ALSO

Full documentation at: <http://www.gnu.org/software/coreutils/printenv> or available locally via: `info '(coreutils) printenv invocation'`

## PRINTF

### NAME

printf – format and print data

### SYNOPSIS

```text
printf FORMAT [ARGUMENT]...
printf OPTION
```

### DESCRIPTION

Print ARGUMENT(s) according to FORMAT, or execute according to OPTION:

- --help
  display this help and exit

- --version
  output version information and exit

FORMAT controls the output as in C printf. Interpreted sequences are:

- \"
  double quote

- \\
  backslash

- \a
  alert (BEL)

- \b
  backspace

- \c
  produce no further output

- \e
  escape

- \f
  form feed

- \n
  new line

- \r
  carriage return

- \t
  horizontal tab

- \v
  vertical tab

- \NNN
  byte with octal value NNN (1 to 3 digits)

- \xHH
  byte with hexadecimal value HH (1 to 2 digits)

- \uHHHH
  Unicode (ISO/IEC 10646) character with hex value HHHH (4 digits)

- \UHHHHHHHH
  Unicode character with hex value HHHHHHHH (8 digits)

- %%
  a single %

- %b
  ARGUMENT as a string with `` escapes interpreted, except that octal escapes are of the form \0 or \ONNN

and all C format specifications ending with one of dioXxXfeEgGcs, with ARGUMENTs converted to proper type first. Variable widths are handled.

NOTE: your shell may have its own version of printf, which usually supersedes the version described here. Please refer to your shell's documentation for details about the options it supports.

### AUTHOR

Written by David MacKenzie.

### REPORTING BUGS

GNU coreutils online help: <http://www.gnu.org/software/coreutils/> Report printf translation bugs to <http://translationproject.org/report.html>

### COPYRIGHT

Copyright 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>. This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

### SEE ALSO

(3)

Full documentation at: <https://www.gnu.org/software/libc/manual/html_node/printf-Invocation.html> or available locally via: `info '(coreutils) printf invocation'`

## PRLIMIT

### NAME

prlimit - get and set process resource limits

### SYNOPSIS

```text
prlimit [options] [--resource[=limits] [--pid PID]
prlimit [options] [--resource[=limits] command [argument...]
```

### DESCRIPTION

Given a process id and one or more resources, **prlimit** tries to retrieve and/or modify the limits.

When *command* is given, **prlimit** will run this command with the given arguments.

The *limits* parameter is composed of a soft and a hard value, separated by a colon (:), in order to modify the existing values. If no *limits* are given, **prlimit** will display the current values. If one of the values is not given, then the existing one will be used. To specify the unlimited or infinity limit (RLIM_INFINITY), the -1 or ‘unlimited’ string can be passed. Because of the nature of limits, the soft limit must be lower or equal to the high limit (also called the ceiling). To see all available resource limits, refer to the RESOURCE OPTIONS section.

- *soft:hard* Specify both limits.
- *soft:* Specify only the soft limit.
- *:hard* Specify only the hard limit.
- *value* Specify both limits to the same value.

### GENERAL OPTIONS

- -h, --help
  Display help text and exit.

- --noheadings
  Do not print a header line.

- -o, --output list
  Define the output columns to use. If no output arrangement is specified, then a default set is used. Use --help to get a list of all supported columns.

- -p, --pid
  Specify the process id; if none is given, the running process will be used.

- --raw
  Use the raw output format.

- --verbose
  Verbose mode.

- -V, --version
  Display version information and exit.
