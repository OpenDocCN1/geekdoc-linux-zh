# Advanced Bash–Scripting Guide

tagged field (usually a numerical), and writes the result to stdout. The files to be joined
should be sorted according to the tagged field for the matchups to work properly.

File: 1.data

100 Shoes
200 Laces
300 Socks

File: 2.data

100 $40.00
200 $1.00
300 $2.00

```
bash$ join 1.data 2.data
File: 1.data 2.data

100 Shoes $40.00
200 Laces $1.00
300 Socks $2.00
```

The tagged field appears only once in the output.

head

lists the beginning of a file to stdout (the default is 10 lines, but this can be changed). It has a number of interesting options.

Example 12–10. Generating 10-digit random numbers

```
#!/bin/bash
# rnd.sh: Outputs a 10-digit random number

# Script by Stephane Chazelas.
nhead -c4 /dev/urandom | od -N4 -tu4 | sed -ne 'ls.*' //p

# ====================================================================
# Analysis
# =

# head:
# -c4 option takes first 4 bytes.

# od:
# -N4 option limits output to 4 bytes.
# -tu4 option selects unsigned decimal format for output.

# sed:
# -n option, in combination with "p" flag to the "s" command,
# outputs only matched lines.
```

# 12.4. Text Processing Commands