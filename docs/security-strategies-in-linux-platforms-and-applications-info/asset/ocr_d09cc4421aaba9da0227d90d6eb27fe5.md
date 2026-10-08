# PART 3 | Building a Layered Linux Security Strategy

Vulnerability (vuln). The scripts in the vulnerability category are all testing for known vulnerabilities. Expect the number of scripts in this category to grow on a regular basis. In fact, the scripts in this category might be the most important reason to use beta versions of nmap software. The following example tries a SQL injection on a target HTTP server:

```
# nmap --sql-injection 192.168.100.1
```

The scripts as listed all may fall under multiple categories. Because new scripts and each switch are under development, assume this is just a partial list. There may be a dozen or more scripts available in several of these areas. Scripts can be bundled together: for example, a command like the following applies all scripts associated with a scan of the HTTP service:

```
# nmap --script=http-* 192.168.100.1
```

If the given script is misspelled or is not otherwise available, the nmap command should return an error with the following message related to the script:

> did not match a category, filename, or directory

# Integrity Checks of Installed Files and Executables

Once you have a production system, it's important to monitor that system for changes. Of course, you should not be alarmed every time a new log is added to the /var/log/ directory. However, changes to critical files such as those in the /boot/ and /sbin/ directories may indicate a more serious problem. To detect such changes, you need to know how to check the integrity of target systems

Sure, you could just set a checksum on potentially vulnerable partitions or volumes, but that would be imprecise. If there's a problem, checksum would not specify the files that have changed.

The first method to check the integrity of a system is based on the integrity of installed packages. To that end, commands based on package management systems such as the Red Hat Package Manager (rpm) and the Debian package management program (dpkg) can help.

But the default configuration based on a package installation is not precise. It highlights problems with normal changes to standard configuration files. Sure, you could keep a list of these changes, but if a black-hat hacker were to get into system and change those files further, there would be no way to tell just using management commands.

That is the reason behind using integrity checkers as Tripwire and the Advanced Intrusion Detection Environment (AIDE). In general, you'll want to use such integrity checkers to log the configuration associated with a baseline before putting such systems online. Then, such integrity checkers can be run on a regular basis. When properly configured, they can highlight any unintended changes to the baseline configuration.