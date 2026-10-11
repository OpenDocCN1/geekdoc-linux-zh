# Example 13-12 Sample cronce File (Continued)

```
#
# Field 1: Comma separated list of hours (0-23) or `*` when this should be run.
#
# Field 2: Comma separated list of days of month or `*` when this should be run.
#
# Field 3: Comma separated list of days of week or `*` when this should be run. Days of week must be exactly as `date' prints.
#
# Remaining fields: Scripts to execute
#
0,8,16 * * * check_known
2 * * check_accounts check_roots check_netro check_anonftp
1 * * check_perms check_signatures check_group check_passed
3 * Mon check_inetd check_exports check_aliases check_path check_cron
2 * Sun find_files
2 1 * crack_run
```

Two sample lines from root's crontab are shown in Example 13-13. It is possible to specify a particular tigercron file on the command line.

# Example 13-13 Sample crontab Entries for tigercron

```
0 * * * * /usr/local/tiger/tigercron >/dev/null 2>l
0 * * * * /usr/local/tiger/tigercron alternate.cronc >/dev/null 2>l
```

tigercron uses variables in the order specified in Table 13.8 to locate the tiger home directory.

# Which Scripts Should I Run?

Before we go any farther, let's take a moment to discuss which scripts you might want to run, and how often. If you have multiple machines, you can set up different cronrc files for each type of system. You may have machines used for development by users (that's what they tell you they are doing, anyway)

| Option | Value |
|:-|:-|
| -B | Specify Basedir for tiger. If this option is used, it takes priority over the other two methods. |
| TIGERHOMEDIR | tiger will check if your UNIX shell has an environment variable of TIGERHOMEDIR; this value, if present, has priority over TigerInstallDir. |
| TigerInstallDir | If neither of the other options is set, this value is used. TigerInstallDir is the value assigned to TIGERHOME in the Makefile before installing. This value is copied into all the scripts when tiger is installed with make. |