the curtains, it invokes the installp command. The SMIT easy_install fastpath is another option that requires fewer keystrokes than install_software.

installp processes an IBM-proprietary package format called Backup File Format, or bff, as well as an older version of the RPM format used by many Linux systems. Unfortunately, installp is missing many features that spoiled administrators have come to take for granted, such as package installation from a network depot and even effective package querying. We always use smit install_software or smit easy_install when we add packages to our AIX systems.

AIX’s lslpp command lists the installed software packages, which IBM refers to as "filesets." lslpp -l all lists all software products on the system—you can also use the smit list_installed_sw fastpath to similar effect. Installed software has state and type codes that indicate the condition and origin of each package. The state can be one of applied, broken, committed, locked, obsolete, or inconsistent. The type is an installp fileset, product, component, feature, RPM, or fix.

# 12.9 REVISION CONTROL

Mistakes are a fact of life. Therefore, it’s important to keep track of the configuration changes you make so that when these changes cause problems, you can easily revert to a known-good configuration. In this section we discuss some common ways of managing changes at the level of individual files. Choose the tools that match your needs and the complexity of your site.

# Backup file creation

This command probably looks familiar:

```
$ cp bigfile.conf bigfile.bak
```

It probably seems a bit shameful, as well—surely, real system administrators do something more sophisticated?

In fact, there’s much to be said in favor of this kind of impromptu backup. Backup files are simple to create, easy to diff, and they create an audit trail, at least to the extent that backup files can be ordered by modification time. They require no additional software, and there’s no possibility that someone will leave the backup system in an ambiguous state.

We suggest a couple of tweaks, however. It’s best to create backup files by moving the original file aside to its new name with mv and then copying it back to its original name. Use cp -p to preserve the file’s attribute settings. This procedure preserves the original file’s modification time and handles cases in which a process has an open reference to the original file.

Better yet, add a short scriptlet like the one below to your ~/.bash_profile or ~/.profile file. It defines a backup "command" (a bash function, really) that picks a backup filename and does the switcheroo for you.