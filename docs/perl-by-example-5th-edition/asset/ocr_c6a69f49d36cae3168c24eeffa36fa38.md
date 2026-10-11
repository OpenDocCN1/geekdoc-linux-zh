# EXAMPLE 10.42 (CONTINUED)

```
The Script
# Scriptname: inplace.plx

while (<ARGV>) { # Open ARGV for reading
 tr/a-z/A-Z/;
 print; # Output goes to file currently being read in-place
 close ARGV if eof;
}
```

Output:
$ perl -i.-bak inplace.plx names.txt
IGOR CHEVSKY
NORMA CORDER
JENNIFER COWAN
JOHN DELOACH
FRED FARDBARKE
LORI GORTZ
PACO GUTIERREZ
EFHRAIM HARDY
JAMES IKEDA

```
more names.txt.bak
igor chevesky
norma corder
jennifor cawan
john deloach
fred fardbarkle
lori goztz
paco gutirrez
ephram hardy
james ikeda
```

# EXPLANATION

+   1 The contents of the original text file, called names.txt, is printed.
+   2 The while loop is entered. The ARGV filehandle will be opened for reading. The ARGV filehandle represents the file coming in from the command line, names.txt.
+   3 All lowercase letters are translated to uppercase letters in the file being processed (tr function).
+   4 The print function sends its output to the file being processed in place.
+   5 The ARGV filehandle will be closed when the end of file is reached. This makes it possible to reset line numbering for each file when processing multiple files or to mark the end of files when appending.
+   6 The -i in-place switch is used with an extension, .bak. The names.txt file will be edited in place and the original file will be saved in names.txt.bak. The names.txt file has been changed, illustrating that the file was modified in place.
+   7 The names.txt.bak file was created as a backup file for the original file. The original file, names.txt, was changed in place.