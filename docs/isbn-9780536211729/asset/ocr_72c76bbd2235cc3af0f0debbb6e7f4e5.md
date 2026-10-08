+   - **New and modified user accounts**—New accounts in `/etc/passwd` and processes running under new or unexpected user IDs as shown by `ps` are indications of new accounts. Accounts with suddenly missing passwords indicate an open account.
- **User accounting records**—Unusual user accounting reports, inexpliable logins, missing or edited log files (such as `/var/log/lastlog`, `/var/log/pacct`, or `/var/log/usracct`), and irregular user activity are signs of trouble.
- **Changes to root or user accounts**—A serious sign is if a user's Login environment is modified or damaged to the point that the account is inaccessible. Of particular concern are changes to users' `.rhost` and `.forward` files, and changes to their `PATH` environment variable.
- **Loss of account access**—Similar to changes to a user's login environment is intentional access denial, whether by changing the account password, by removing the account, or, for regular users, by changing the runlevel to single-user mode.

# 9.2.5 Security Audit Tool Indications

Security audit tool indications include filesystem integrity mismatches, file-size changes, changes to file-permission mode bits, new `setuid` and `setgid` programs, alerts from Intrusion detection tools such as Snort, and service monitoring data.

Files with mismatched hash signatures can be files that are new, files whose lengths or creation or modification dates have changed, and files whose access modes are altered. Of particular concern are newly installed trojan horse programs. Frequent targets for replacement are programs managed by `inetd` or `xinetd`, `inetd` or `xinetd` itself, `ls`, `ps`, `netstat`, `ifconfig`, `telnet`, `login`, `su`, `ftp`, `syslogd`, `du`, `df`, `sync`, and the `libc` library.

# 9.2.6 System Performance Indications

System performance indications include unusually high load averages and heavy disk access.

Unexplained, poor system performance could be caused by unusual process activity, unusually high load averages, excessive network traffic, or heavy filesystem access.

If your system shows signs of a successful compromise, don't panic. Don't reboot the system—important information could be lost. Simply physically disconnect the system from the Internet.

# 9.3 What to Do If Your System Is Compromised

The paper "Steps for Recovering from a UNIX Root Compromise," available from CERT at http://www.cert.org/tech_tips/, RFC 2196, "Site Security Handbook", and the SANS publication "Computer Security Incident Handling: Step by Step" discuss procedures to follow in the event of a successful security breach. These documents present more formal proce-