![](bbox=[0.12, 0.04, 0.27, 0.1])

windows-privesc-check v2.0 ([http://pentestmonkey.net/windows-privesc-check](http://pentestmonkey.net/windows-privesc-check))

Usage: windows_privesc_check.exe (--dump [ dump opts] | --dumptab | --audit) [examine opts] [host opts] -o report-file-stem

+   Options:
+   - --version show program's version number and exit
+   - -h, --help show this help message and exit
+   - --dump Dumps info for you to analyse manually
+   - --dumptab Dumps info in tab-delimited format
+   - --audit Identify and report security weaknesses
+   - --pyshe ll Start interactive python shell

+   examine opts:
+   At least one of these to indicate what to examine (\*=not implemented)
+   - -a, --all All Simple Checks (non-slow)
+   - -A, --allfiles All Files and Directories (slow)
+   - -D, --drives Drives
+   - -e, --reg_keys Misc security-related reg keys
+   - -E, --eventlogs Event Log\*
+   - -F INTERESTING_FILE_LIST, --interestingfiledir=INTERESTING_FILE_LIST
+   - Changes -A behaviour. Look here INSTEAD
+   - -F INTERESTING_FILE_FILE, --interestingfilefile=INTERESTING_FILE_FILE
+   - Changes -A behaviour. Look here INSTEAD. On dir per line
+   - -G, --groups Groups
+   - -H, --shares Shares
+   - -I, --installed_software Installed Software
+   - -j, --tasks Scheduled Tasks
+   - -K, --drivers Kernel Drivers
+   - ...

*Listing 550 - Output executable by PyInstaller*

This tool accepts many options, but we will walk through some quick examples. First, we will list information about the user groups on the system. We'll specify the self-explanatory `--dump` to view output, and `-G` to list groups.

```
c:\\Tools\\privelege_escalation\\windows-privesc-check-master> **windows-privesc-check2.exe**
--dump -G
windows-privesc-check v2.0 (http://pentestmonkey.net/windows-privesc-check)

[i] TSUserEnabled registry value is 0. Excluding TERMINAL SERVER USER

Considering these users to be trusted:
\* BUILTIN\\Power Users
\* BUILTIN\\Administrators
\* NT SERVICE\\TrustedInstaller
\* NT AUTHORITY\\SYSTEM

[i] Running as current user. No logon creds supplied (-u, -D, -p).
...
========== Starting Audit at 2019-09-22 12:45:56 ==========
```