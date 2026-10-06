# Advanced Bash–Scripting Guide

```
# Use two decimal places for dollars and cents.
echo
echo "monthly payment = \$payment" # Echo a dollar sign in front of amount.
echo
```

exit 0

+   # Exercises:
# 1) Filter input to permit commas in principal amount.
# 2) Filter input to interest to be entered as percent or decimal.
# 3) If you are really ambitious,
# expand this script to print complete amortization tables.

# Example 12-3. Base Conversion

```
###############################################################################
# Shellscript: base.sh - print number to different bases (Bourne Shell)
# Author : Heiner Steven (heiner.steven@odn.de)
# Date : 07-03-95
# Category : Desktop
# $Id:base.sh.v 1.2 2000/02/06 19:55:35 heiner Exp $\$
###############################################################################
# Description
```

# Changes
# 21-03-95 stv fixed error occurring with 0xb as input (0.2)
###############################################################################

> # Used in this document with the script author's permission.
# --> Comments added by document author.

```
NOARGS=65
PN=$(basename "$0") # Program name
VER=$(echo 'RRevision: 1.2 $' | cut -d ' ' -f2) #==VER=1.2

Usage() {
  echo "$PN" - print number to different bases, $VER (stv '95)
  usage: $PN [ number ... ]
```

If no number is given, the numbers are read from standard input.
A number may be
binary (base 2) starting with 0b (i.e. 0b1100)
octal (base 8) starting with 0 (i.e. 0114)
adecimal (base 16) starting with 0x (i.e. 0xc)
decimal otherwise (i.e. 12) >&2

```
exit $NOARGS
# --> Function to print usage message.

Msg() {
  for i #== in [list] missing.
  echo "$PN: $1" >2
done
```

```
Fatal () { Msg "$0"; exit 66; }
```

```
PrintBases () {
# Determine base of the number
```

# 12.7. Terminal Control Commands

188