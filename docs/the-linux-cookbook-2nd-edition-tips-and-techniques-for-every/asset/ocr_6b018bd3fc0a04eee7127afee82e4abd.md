⇒ Here are two ways to use this.

+   • To remove the newline characters from the text file `autoexec.bat`, type:
+   
+     `$ fromdos autoexec.bat` [RET]
+   
+   • To add newline characters to all of the text files with a `.tex` extension in the current directory, type:
+   
+     `$ todos *.tex` [RET]

**NOTES:** Both commands write directly to the files you specify. To make a backup of the original file, use the `-b` option; before the conversion, this writes a copy of each specified file with a `.bak` file name extension.

# METHOD #2

Use the `col` filter to filter out carriage returns from text, as described in Recipe 13.19 [Removing Carriage Return Characters], page 310.

⇒ To filter out the carriage returns from the file `README.TXT`, writing to a new file called `readme.txt`, type:

```
$ col < README.TXT > readme.txt [RET]
```

# METHOD #3

Another way to convert text from DOS is to use the `tr` filter to delete the carriage returns (see Recipe 13.4 [Transposing Characters in Text], page 316).

⇒ To filter out the carriage returns from the file `dos-version.txt`, writing to a new file `unix-version.txt`, type:

```
$ tr -d '\r' < dos-version.txt > unix-version.txt [RET]
```

**NOTES:** To do the reverse of this—to convert text from UNIX to DOS—I have been told that simply opening the file in the DOS text editor program called EDIT, and then saving the file and exiting, will work. This will automatically add the requisite carriage returns to the end of each line.

# 26.5 Converting Microsoft Word Files

word2x:

DEB: word2x
RPM: word2x
WWW: http://word2x.sourceforge.net/