In this case, a package has been installed. As expected, its scripts are executed. Next, let’s upgrade this package:

```
# rpm -U bot her-3.5-1.i386.rpm
This is the bot her 3.5 preinstall script
This is the bot her 3.5 postinstall script
This is the bot her 2.7 preuninstall script
This is the bot her 2.7 postuninstall script
#
```

This is a textbook example of the sequence of events during an upgrade. The new version of the package is installed (as shown by the pre- and postinstall scripts being executed). Finally, the previous version of the package is removed (showing the pre- and postuninstall scripts being executed). There are really no surprises here. It worked just the way it was meant to.

This time, let’s use the -noscripts option when the time comes to perform the upgrade:

```
# rpm -i bot her-2.7-1.i386.rpm
This is the bot her 2.7 preinstall script
This is the bot her 2.7 postinstall script
#
```

Again, the first package is installed and its scripts are executed. Now let’s try the upgrade using the -noscripts option:

```
# rpm -U -noscripts bot her-3.5-1.i386.rpm
This is the bot her 2.7 preuninstall script
This is the bot her 2.7 postuninstall script
#
```

The difference here is that the -noscripts option prevented the new package’s scripts from executing. The scripts from the package being erased were still executed.