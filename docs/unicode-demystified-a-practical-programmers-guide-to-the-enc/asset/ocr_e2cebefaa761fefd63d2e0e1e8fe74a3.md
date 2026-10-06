# cmp

Checks whether two files differ

cmp [options] file1 [file2]

The cmp utility uses a byte-by-byte comparison of file1 and file2. If the files differ, cmp outputs the location at which the first difference occurs. Unlike diff (page 1149), cmp works with binary and as ASCII files.

The cmp utility returns an exit status of 0 if the files are the same and 1 if they are different. An exit status > 2 means that an error occurred.

# Arguments

The file1 and file2 arguments identify the two files to compare. If file2 is omitted, cmp uses standard input instead. Using a filename of - for either file1 or file2 causes cmp to read standard input in place of that file.

# Options

+   --ignore-initial=n -i Skips the first n bytes in both files before beginning the comparison.

+   --print-chars -c Shows the bytes at the first location where the files differ. The byte at that location in each file is displayed as an octal value and an ASCII character. Nonprinting ASCII characters are displayed symbolically.

+   --silent or -s Suppresses output from cmp. Use this option when you are interested in only the exit status from the comparison.

+   --verbose -l Instead of stopping at the first byte that differs, continues comparing the two files and displays both the locations and values of every byte that differs in the two files. Locations are displayed as decimal offsets from the beginning of the files, and byte values are displayed in octal. The comparison terminates when an EOF is encountered on either file.

# Notes

The cmp utility only sets the exit status; it does not display any output if the files are identical.