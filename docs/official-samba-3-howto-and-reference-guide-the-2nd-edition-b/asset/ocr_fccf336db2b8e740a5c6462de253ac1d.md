There is no difficulty with using your own customized print commands with the traditional printing systems. However, if you do not wish to roll your own, you should be well informed about the default built-in commands that Samba uses for each printing subsystem (see Table 20.1). In all the commands listed in the last paragraphs, see parameters of the form %X. These are macros, or shortcuts, used as placeholders for the names of real objects. At the time of running a command with such a placeholder, Samba will insert the appropriate value automatically. Print commands can handle all Samba macro substitutions. In regard to printing, the following ones do have special relevance:

+   * %s, %f — the path to the spool file name.
+   * %p — the appropriate printer name.
+   * %J — the job name as transmitted by the client.
+   * %c — the number of printed pages of the spooled job (if known).
+   * %z — the size of the spooled print job (in bytes).

The print command must contain at least one occurrence of %s or %f. The %p is optional. If no printer name is supplied, the %p will be silently removed from the print command. In this case, the job is sent to the default printer.

If specified in the [global] section, the print command given will be used for any printable service that does not have its own print command specified. If there is neither a specified print command for a printable service nor a global print command, spool files will be created but not processed! Most importantly, print files will not be removed, so they will consume disk space.

Printing may fail on some UNIX systems when using the nobody account. If this happens, create an alternative guest account and give it the privilege to print. Set up this guest account in the [global] section with the guest account parameter.

You can form quite complex print commands. You need to realize that print commands are just passed to a UNIX shell. The shell is able to expand the included environment variables as usual. (The syntax to include a UNIX environment variable Variable in the Samba print command is %$Variable. ) To give you a working print command example, the following will log a print job to /tmp/print.log, print the file, then remove it. The semicolon (";") is the usual separator for commands in shell scripts:

```
print command = echo Printing %s >> /tmp/print.log; lpr -P %f -z p %s; rm %s
```

You may have to vary your own command considerably from this example depending on how you normally print files on your system. The default for the print command parameter varies depending on the setting of the printing parameter. Another example is:

```
print command = /usr/local/samba/bin/myprintscript %p %s
```