# Advanced Bash-Scripting Guide

objdump
Displays information about an object file or binary executable in either hexadecimal form or as a disassembled listing (with the -d option).

```
bash objdump -d /bin/ls
/bin/ls:    file format elf32-1386

Disassembly of section .init:

080490bc.<init>:
080490bc:    55      push %ebp
080490bd:      e9 e5    mov %esp,%ebp
```

mookie
This command generates a "magic cookie", a 128-bit (32-character) pseudorandom hexadecimal number, normally used as an authorization "signature" by the X server. This also also available for use in a script as a "quick dirty" random number.

```
random000=$(mookie)
Of course, a script could use md5sum for the same purpose.

# Generate md5 checksum on the script itself.
random001=$(md5sum $ | awk '{print $1}')
# Uses 'awk' to strip off the filename.
The mookie command gives another way to generate a "unique" filename.
```

# Example 16-62. Filename generator

```
#!/bin/bash
# tempfile-name.sh:   temp filename generator
BASE_STR=`mookie`      # 32-character magic cookie.
# Arbitrary position in magic cookie string.
POS=1                 # Get LEN characters.
LEN=5
prefix=temp           # This is, after all, a "temp" file.
# For more "uniqueness", generate the
#++ prefix using the same method
# as the suffix, below.
suffix=${BASE_STR:$POS:$LEN}  # Extract a 5-character string,
#++ starting at position 11.
tempfile-name=$prefix.$suffix  # Construct the filename.
echo "Temp filename = "$tempfile_name"

# sh tempfile-name.sh
# Temp filename = temp.el9ea

# Compare this method of generating "unique" filenames
#++ with the 'date' method in ex51.sh.

exit 0
```

Chapter 16. External Filters, Programs and Commands