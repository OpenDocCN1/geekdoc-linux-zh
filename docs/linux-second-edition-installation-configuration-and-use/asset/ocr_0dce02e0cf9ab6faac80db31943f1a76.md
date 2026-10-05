# ALPHABETICAL COMMAND REFERENCE 449

-z or --elide-empty-files
prevents the creation of empty files. Without this option, empty files can occur.
espec when the first line of the source file matches the search pattern.

# Examples

```
user csplit -k f part. total.txt 100 (*)
```

splits total.txt into the files part.00, part.01, and so on. Each file is 100
long.

```
user csplit -k f part. total.txt '/^% ---/-' (*)
```

as above, except that the file is split every time a line begins with the text ---

# cut [options] file

cut extracts the columns specified by the options from each line of a text.

+   -b list
  xtracts the characters specified in a list. Single characters may be separated by
commas (but not by spaces). Alternatively, entire ranges can be specified, such
as -b 3-6,9,11-15.

+   -f list --fields
  as above, but applying to fields (data records) which must be separated by tab
characters.

+   -d --delimiter character
  specifies the separation character for -f; this character is to be used instead of
tab character.

+   -s or --only-delimited
  eliminates all lines that do not contain data that corresponds to the -f option
Cannot be used together with -b.

# Example

```
ls -l | cut -b 1-11,56-
```

uses cut to filter the list obtained with ls. As a result, only the access rights and
the file names (characters 1 to 11 and all characters from the 56th character onwards)
are displayed.

# date [options] time

date displays the current date and time or changes them. (Changes can only be ber
ried by root.) date can display the time in various formats (see the man texts).

+   -s sets the date and/or time (instead of displaying them).