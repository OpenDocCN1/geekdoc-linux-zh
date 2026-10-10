shell pattern (see the section “Shell Patterns” in Chapter 4). If you omit the filename, the utility takes input from the standard input.

# OPTIONS

**Use This Option** **To Do This**
-b range, --bytes==range Output only the bytes specified by range (see the Ranges table in this section).
-c range, --characters==range Output only the characters specified by range (see the Ranges table in this section).
-d, --delimiter==character Use character instead of tab for the field delimiter.
-f range, --fields==range Output only the fields specified by range (see the Ranges table in this section).
--help Display this help and exit.
--output-delimiter==string Use string as the output delimiter. The default is to use the input delimiter.
-s, --only-delimited Print only those lines that contain delimiters.
--version Show the version number.

# RANGES

**Range** **Description**
n The nth byte, character, or field
-m A range extending from the first to the mth byte, character, or field
n- A range extending from the nth byte, character, or field to the end of line
n-m A range extending from the nth to the mth byte, character, or field