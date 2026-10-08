# Advanced Bash-Scripting Guide

```
# Exercises:
# 1) Filter input to permit commas in principal amount.
# 2) Filter input to permit interest to be entered as percent or decimal.
# 3) If you are really ambitious,
# expand this script to print complete amortization tables.
```

Example 16-48. Base Conversion

```
#!/bin/bash
######################################################################
# Shellscript: base.sh - print number to different bases (Bourne Shell)
# Author : Heiner Steven (heiner.steven@odn.de)
# Date : 07-03-95
# Category : Desktop
# $ID: base.shv in 2000/02/06 19:55:35 heiner Exp $
# ==> Above line is RCS ID info.
######################################################################
# Description

# Changes
# 21-03-95 stv fixed error occurring with 0xb as input (0.2)
######################################################################

# ==> Used in ABS Guide with the script author's permission.
# ==> Comments added by ABS Guide author.

NOARGS=85
PN=$(basename "$0") # Program name
VER=$('Revision: 1.2 $' | cut -d '\'' -f2) # ==> VER=1.2

Usage [ ]
  echo "$PN - print number to different bases, $VER (stv '95)'
  usage: $PN ..."

If no number is given, the numbers are read from standard input.
A number may be
  binary (base 2)        starting with Ob (i.e. 0b1100)
  octal (base 8)         starting with 0 (i.e. 014)
  hexadecimal (base 16)  starting with 0x (i.e. 0xc)
  decimal               otherwise (i.e. 12") >&2
  ==> $NOARGS
) ==> Prints usage message.

Msg () {
  for i == in [list] listing. Why?
  do echo "$PN: $1" >&2
  done
}

Fatal () {
  Msg "$0"; exit 66;
}

PrintBases () {
  # Determine the base of the number
  for i == in [list]...
  do # ==> so operates on command-line args(s).
    case "$i" in
      ibase=2)          # binary
      0x['[a-f][A-F]*)  # hexadecimal
      ibase=16);
```

Chapter 16. External Filters, Programs and Commands