# Symptoms Suggesting That the System Might Be Compromised

+   New files and directories—Besides files with suddenly bad digital signatures, you might discover new files and directories. Especially suspicious are filenames starting with one or more dots and legitimate-sounding filenames appearing in unlikely places.

+   setuid and setgid programs—New setuid files, and newly set setgid files, are a good place to start looking under the hood for problems.

+   Missing files—Missing files, particularly log files, indicate a problem of some kind.

+   Rapidly changing filesystem sizes, as shown by df—If the machine is compromised, rapidly growing filesystems might be a sign of a hacker's monitoring program producing large log files.

+   Modified public file archives—Check the contents of your web and FTP areas for new or modified files.

+   New files or directories in /dev—CERT warns especially to check for the presence of new ASCII files or directories in /dev; these are typically Trojan programs' configuration files.

# User Account Indications

User account indications include new user accounts, changes to the passwd file, unusual activity in the user process accounting reports or missing process accounting reports, changes to user files—especially environmental files—and loss of account access:

+   New and modified user accounts—New accounts in /etc/passwd and processes running under new or unexpected user IDs as shown by ps are indications of new accounts. Accounts with suddenly missing passwords indicate an open account.

+   User accounting records—Unusual user accounting reports, inexplicable logins, missing or edited log files (such as /var/log/lastlog, /var/log/pacct, or /var/log/utracct), and irregular user activity are signs of trouble.

+   Changes to root or user accounts—A serious sign is if a user's login environment is modified or damaged to the point that the account is inaccessible. Of particular concern are changes to users' .rhost and .forward files, and changes to their PATH environment variable.

+   Loss of account access—Similar to changes to a user's login environment is intentional access denial, whether by changing the account password, by removing the account, or, for regular users, by changing the runlevel to single-user mode.