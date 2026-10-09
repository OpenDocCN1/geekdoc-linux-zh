lines in the file. Those type of files are Windows/DOS formatted. Unix-like operating systems simply use the LF character to terminate a line. Sometimes this can cause issues. To convert the file to a unix-like format, use dos2unix. To examine the line termination characters use "cat -A" or the "file" command.

```
```
$ cat -A from-my-windows-buddy.pl
#!/usr/bin/perl\M
print "This is a cross-platform perl script!\n"\M$
$ ./from-my-windows-buddy.pl
-bash: ./from-my-windows-buddy.pl: /usr/bin/perl\M: bad interpreter: No such file or directory
$ dos2unix from-my-windows-buddy.pl
dos2unix: converting file from-my-windows-buddy.pl to UNIX format . . .
$ cat -A from-my-windows-buddy.pl
#!/usr/bin/perl$
print "This is a cross-platform perl script!\n"$
$ ./from-my-windows-buddy.pl
This is a cross-platform perl script!
$ file other-file.txt
other-file.txt: ASCII text, with CRLF line terminators
$ dos2unix other-file.txt
dos2unix: converting file other-file.txt to UNIX format . . .
$ file other-file.txt
other-file.txt: ASCII text
```

```