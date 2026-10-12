-I *directory*—Directories specified by -I are prepended to the search path for modules (@INC).

-i[*extension*]—This indicates that files are to be edited in place. If the extension is provided, the original is backed up with that extension. Otherwise, the original file is overwritten.

-l[*octnum*]—Enables automatic line-ending processing, which means that end-of-line characters are automatically removed from input and put back on to output. If the optional octal number is unspecified, this is just the newline character.

-m[*-module*] or -M[*-module*]—Loads the specified module before running your script. There’s a subtle difference between m and M. See perlrun for more details.

-n—Causes Perl to loop around your script for each file provided to the command line. Does not print the output. The following example, from perlrun, deletes all files older than a week:

```
$ find . -mtime +7 -print | perl -nle 'unlink;'
```

-P—This causes your script to be run through the C preprocessor before compilation by Perl.

-p—This is just like -n except that that each line is printed.

-S—This searches for the script using the PATH environment variable.

-s—This performs some command-line switch parsing and puts the switch into the corresponding variable in the Perl script. For example, the following script prints '1' if run with the -foobar switch. Your Perl code might look like this:

```
#!/usr/bin/perl -s
print $foobar;
```

When you execute it, you would enter

```
$ ./myperl -foobar
```

-T—This enables taint checking. In this mode, Perl assumes that all user input is tainted, or insecure, until the programmer tells it otherwise. This helps protect you from people trying to exploit security holes in your code and is especially important when writing CGI programs.

-U—This enables you to do unsafe things in your Perl program, such as unlinking directories while running as superuser.

-u—An available, but obsolete switch to tell Perl to dump core after compiling a program.

-V—This prints a summary of the major Perl configuration values and the current value of @INC.

-V: *names*

This parameter displays the value of the names configuration variable.

-v—This prints the version and patch level of your Perl executable. For example,

```
$ perl -v
This is perl, v5.8.4 built for i386-linux-thread-multi
(with 1 registered patch, see perl -V for more detail)
```