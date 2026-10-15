ignore or override a file of default rules by creating a new file with the same name in the custom rules directory.

The master configuration file for udev is /etc/udev/udev.conf; however, the default behaviors are reasonable. The udev.conf files on our example distributions contain only comments, with the exception of one line that enables error logging.

Sadly, because of political bickering among distributors and developers, there is little rule synergy among distributions. Many of the filenames in the default rules directory are the same from distribution to distribution, but the contents of the files differ significantly.

Rule files are named according to the pattern nn-description.rules, where nn is usually a two-digit number. Files are processed in lexical order, so lower numbers are processed first. Files from the two rules directories are combined before the udev daemon, udevd, parses them. The .rules suffix is mandatory; files without it are ignored.

Rules are of the form

```
match_clause, [match_clause, ...] assignment_clause [,assignment_clause ...]
```

The match_clauses define the situations in which the rule is to be applied. Each match clause consists of a key, an operator, and a value. For example, the clause ATTR{size}=="1974271" was referred to above as a potential component of a rule; it selects all devices whose size attribute is exactly 1,974,271.

Most match keys refer to device properties (which udevd obtains from the /sys filesystem), but some refer to other context-dependent attributes, such as the operation being handled (e.g., device addition or removal). All match clauses must match in order for a rule to be activated.

Table 13.8 shows the match keys understood by udev.

# Table 13.8 Udev match keys

| Match key | Function |
|---|---|
| ACTION | Matches the event type, e.g., add or remove |
| DEVPATH | Matches a specific device path |
| KERNEL* | Matches the kernel's name for the device |
| SUBSYSTEM* | Matches a specific subsystem |
| DRIVER* | Matches the driver used by a device |
| ATTR{filename}* | Matches a device's sysfs values; the filename is a leaf in the sysfs tree that corresponds to a specific attribute |
| ENV{key} | Matches the value of an environment variable |
| TEST[omask] | Tests whether a file exists; the omask is optional |
| PROGRAM | Runs an external command; matches if the return code is 0 |
| RESULT | Matches the output of the last call through PROGRAM |

a. A plural version is also available. It searches up the device path to match the value.