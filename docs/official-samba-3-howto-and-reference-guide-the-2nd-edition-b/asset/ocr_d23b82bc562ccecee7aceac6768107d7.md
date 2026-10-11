The print command is simply a text string. It will be used verbatim after macro substitutions have been made:

+   • `%s, %f` - the path to the spool file name
+   • `%p` - the appropriate printer name
+   • `%J` - the job name as transmitted by the client.
+   • `%c` - The number of printed pages of the spooled job (if known).
+   • `%z` - the size of the spooled print job (in bytes)

The print command MUST contain at least one occurrence of `%s` or `%f` - the `%p` is optional. At the time a job is submitted, if no printer name is supplied the `%p` will be silently removed from the printer command.

If specified in the [global] section, the print command given will be used for any printable service that does not have its own print command specified.

If there is neither a specified print command for a printable service nor a global print command, spool files will be created but not processed and (most importantly) not removed.

Note that printing may fail on some UNIXes from the `nobody` account. If this happens then create an alternative guest account that can print and set the *guest account* in the [global] section.

You can form quite complex print commands by realizing that they are just passed to a shell. For example the following will log a print job, print the file, then remove it. Note that `?:` is the usual separator for command in shell scripts.

```
print command = echo Printing %s > /tmp/print.log; lpr -P %p %s; rm %s
```

You may have to vary this command considerably depending on how you normally print files on your system. The default for the parameter varies depending on the setting of the *printing* parameter.

Default: For printing = BSD, AIX, QNX, LPNG or PLP :

```
print command = lpr -r -P%p %s
```

For printing = SYSV or HPUX :

```
print command = lp -c -d%p %s; rm %s
```

For printing = SOFTQ :

```
print command = lp -d%p -s %s; rm %s
```

For printing = CUPS : If SAMBA is compiled against libcups, then *printing* = cups uses the CUPS API to submit jobs, etc. Otherwise it maps to the System V commands with the -oraw option for printing, i.e. it uses `lp -c -d%p -oraw; rm %s`. With *printing* = cups. and if SAMBA is compiled against libcups, any manually set print command will be ignored.