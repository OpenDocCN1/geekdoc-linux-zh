```
./OWL/define.c
./OWL/spell.c
./OWL/submit.c
./OWL/utils.c
./OWL/parse.c
./OWL/sendmail.c
./owl.c
./src/calc.c
./src/info.c
./src/fixit.c
./src/massage.c
```

Using the -name option before the -print option can be very handy.

# 3. To find just files that have been modified in the past seven days, I can use -mtime with the argument -7 (including the hyphen):

Click here to view code image

```
$ find . -mtime -7 -name "*.c" -print
./OWL/owl.c
./OWL/simple.editor.c
./OWL/ask.c
./OWL/utils.c
./OWL/sendmail.c
```

If I use just the number 7 (without a hyphen), I will match only files that were modified exactly seven days ago:

Click here to view code image

```
$ find . -mtime 7 -name "*.c" -print
$
```

To find C source files that I haven’t touched for more than 30 days, I use +30:

Click here to view code image

```
$ find . -mtime +30 -name "*.c" -print
./OWL/WordMap/msw-to-txt.c
./OWL/WordMap/newtest.c
./src/calc.c
./src/info.c
./src/fixit.c
./src/massage.c
```

# 4. With find, I now have a tool for looking across vast portions of the file system for specific file types, filenames, and other attributes.

To look across the /bin and /usr directory trees for filenames that contain the pattern cp, I can use the following command:

Click here to view code image

```
$ find /bin /usr -name "*cp*" -print
/bin/cp
/bin/rcp
/usr/bin/cpan
/usr/bin/cpio
/usr/bin/cpp
/usr/bin/cpp-3.3
/usr/bin/cpp-4.0
/usr/bin/escputil
/usr/bin/scp
```