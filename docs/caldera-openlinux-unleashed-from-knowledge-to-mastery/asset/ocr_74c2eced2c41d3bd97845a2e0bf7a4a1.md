+   * -d:foo Runs the script under the control of a debugging or tracing module installed as Devel::foo. For example, -d:DProf executes the script using the Devel::DProf profiler. See perldebug for additional information on the Perl debugger.

+   * -Dflags Sets debugging flags. See perlrun for more details.

+   * -e commandline Indicates that what follows is Perl code. This allows you to enter Perl code directly on the command line rather than running code contained in a file.

```
`perl -e 'print join " ", keys %ENV;'`
```

+   * -Fpattern Specifies the pattern to split on if -a is also in effect. This is “ ” by default, and -F allows you to set it to whatever works for you, such as ‘,’ or ‘;’. The pattern may be surrounded by //, “”, or ‘’.

+   * -h Typing perl -h lists all available command-line switches.

+   * -i[extension] Indicates that files are to be edited in place. If the extension is provided, the original is backed up with that extension. Otherwise, the original file is overwritten.

+   * -Idirectory Directories specified by -I are prepended to the search path for modules (@INC).

+   * -I[octnum] Enables automatic line-ending processing, which means that end-of-line characters are automatically removed from input and put back onto output. If octnum is omitted, this is just the newline character.

+   * -m|-module or -M|-module Executes use module before running your script. There is a subtle difference between m and M. See perlrun for more details.

+   * -n Causes Perl to loop around your script for each file provided to the command line. Does not print the output. The following example, from perlrun, deletes all files older than a week:

```
find . -mtime +7 -print | perl -nle ‘unlink;’
```

+   * -p This is just like -n, except that each line is printed.

+   * -P Causes script to be run through the C preprocessor before compilation by Perl.

+   * -s Performs some command-line switch parsing and puts the switch into the corresponding variable in the Perl script. For example, the following script prints ‘1’ if run with the -fubar switch. Your Perl code might look like:

```
```
#!/usr/bin/perl -s
print $fubar;
```
```

When you execute it, you would enter:

```
`myperl -fubar`
```