# Chapter 8 · Searching, Extracting, and Archiving Data

# Using grep

Certification Objective

If you don't specify a filename, grep uses standard input. This can be useful with pipelines, as described shortly in the section "Redirecting Input and Output.",

The grep command searches for files that contain a specified string and returns the name of the file and (if it's a text file) the line containing that string. You can also use grep to search a file for a specified string. To use grep, you type the command's name, an optional set of options, a regular expression, and an optional filename specification. The grep command supports a large number of options, the most common which appear in Table 8.1.

# TABLE 8.1 Common grep options

| Option (long form) | Option (short form) | Description |
| --- | --- | --- |
| --count | -c | Instead of displaying the lines that contain matches to the regular expression, displays the number of lines that match. |
| --file=file | -f file | This option takes pattern input from the specified file rather than from the command line. The grep command is a shortcut for this option. |
| --ignore-case | -i | You can perform a case-insensitive search, rather than the default casesensitive search, by using the -i or --ignore-case option. |
| --recursive | -R or -r | This option searches in the specified directory and all of the subdirectories rather than simply the specified directory. You can use grep rather than specify this option. |
| --extended-regexp | -E | The grep command uses regular expressions by default. To use an extended regular expression, you can pass this option. Alternatively, you can call egrep rather than grep; this variant command uses extended expressions by default |