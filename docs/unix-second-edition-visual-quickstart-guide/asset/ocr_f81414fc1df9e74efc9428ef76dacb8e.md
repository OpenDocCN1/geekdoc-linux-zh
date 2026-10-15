```
[ejr@hobbes creative]$ more rot13
#! /bin/sh
#
#  If the first item (after the script name) on the command
#  line is save or s, and the second item is a readable file
#  then do the first case.
if [ \( "$1" = "save" -o "$1" = "s" \) -a \( -r "$2" \ ) ]
then
#
#  This case saves the ROT13 output under the same filename with
#  a rot13 extension.
/bin/sed y/abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ/nopqrstuvwxyzabcdefghijklmNOPQRSTUVWXYZ + UVWXYZABCDEF GHIJKLM/ "$2" > "$2".rot13
else
#
#  This case pipes the ROT13 output to more, because a save
#  wasn't specified.
/bin/sed y/abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ/nopqrstuvwxyzabcdefghijklmNOPQRSTUVWXYZ + UVWXYZABCDEF GHIJKLM/ "$1" | more
fi

[ejr@hobbes creative]$
```

Code Listing 17.7 If you want to get really fancy with the script, you can bring together some of the handiest bits of other chapters to make a masterpiece.