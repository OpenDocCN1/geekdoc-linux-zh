# EXPLANATION

+   1 Send five copies of filea and fileb to the printer.
+   2 Specify Shakespeare as the printer where filex will be printed.

# lpr—sends output to a printer (UCB)

```
lpr [ -Pprinter ] [ -#copies ] [ -Cclass ] [ -Jjob ]
    [ -Ttitle ] [ -i [ indent ] ] [ -1234font ] [ -wcols ]
    [ -r ] [ -m ] [ -h ] [ -s ] [ -filter-option ] [ filename ... ]
```

lpr creates a printer job in a spooling area for subsequent printing as facilities become available. Each printer job consists of a control job and one or more data files.

# EXAMPLE A.36

+   1 lpr -#5 filea fileb
+   2 lpr -PShakespeare filex

# EXPLANATION

+   1 Sends five copies of filea and fileb to the printer.
+   2 Specifies Shakespeare as the printer where filex will be printed.

# lpstat—prints information about the status of the LP print service (AT&T)

# lpq—prints information about the status of the printer (UCB)

# ls—lists contents of directory

```
ls [ -abcCdfFgilLmnopqrRStux1 ] [ names ]
```

For each directory argument, ls lists the contents of the directory; for each file argument, ls repeats its name and any other information requested. The output is sorted alphabetically by default. When no argument is given, the current directory is listed.

# EXAMPLE A.37

+   1 ls -alF
+   2 ls -d a*
+   3 ls -i

# EXPLANATION

1 The -a lists invisible files (those files beginning with a dot), the -l is a long listing showing attributes of the file, the -F puts a slash at the end of directory filenames, an * at the end of executable script names, and an @ symbol at the end of symbolically linked files.