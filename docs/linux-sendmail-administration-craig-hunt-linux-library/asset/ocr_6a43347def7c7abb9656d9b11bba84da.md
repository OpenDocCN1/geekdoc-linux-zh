> NOTE In the rest of this chapter, to reduce the size of the listings, the copyright statements that start the files are not printed, but you should be aware that they are.

The first real configuration command in the file is a define statement that assigns a value to the CONFEBINDIR parameter. This parameter stores the path of the directory that holds executable binary files. The Sendmail 8.11 default for CONFBINDIR is /usr/libexec. This define changes the setting to /usr/sbin. Both of these directories exist on Linux systems, but the /usr/sbin directory is the one that is more commonly used to hold system binary files, and in this case it is correct. The CONFBINDIR path is used to locate the smr mailer, which is frequently used as the prog mailer on Linux systems. (The prog mailer, Chapter 12, "Sendmail Security," describes the advantages of using the smr mailer.) A couple of quick commands on our Linux system system show that the correct value for CONFBINDIR is /usr/sbin:

```
$craig$ ls /usr/libexec/smrsh
ls: /usr/libexec: No file or directory
$craig$ ls /usr/sbin/smrsh
/usr/sbin/smrsh
```

The second configuration command is also a define. This is a little more complex. This define is contained inside an ifdef. The ifdef has nothing to do with configuration Sendmail. It is a built-in m conditional command that checks whether or not a variable has already been set to a value. The ifdef command has three fields:

+   * the name of the variable that is being tested
* the action to take if the variable has been set
* the action to take if the variable has not been set

In Listing 5.2, the ifdef tests the variable PROCMAIL_MAILER_PATH. If the variable has already been defined, nothing is done. We know this by the fact that the second field of the ifdef is empty—notice the two commas right in a row (,). If the variable has not been set, the define contained in the third field of the ifdef is executed. It is exactly what happens on our sample system, because we did not assign any value to PROCMAIL_MAILER_PATH in the macro configuration file.

The define assigns the variable PROCMAIL_MAILER_PATH the path value /usr/bin/procmail. This overrides the Sendmail default for PROCMAIL_MAILER_PATH, which is