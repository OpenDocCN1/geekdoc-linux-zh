
## Answer Key

- 4. Answer: **mdprobe** (There are an alternative correct answers.)

- 5. Answer: **mkboot vmlinuz** (An alternative answer is **mkboot /boot/vmlinuz**.)

- 6. Answer: **uname -r** (There are no alternative correct answers.)

- 7. Answers A, D, and E are correct because they all result in the system entering runlevel 1. $s$ is a synonym for 1, and $S$ means that scripts will be run before runlevel 1 is entered. Answer B is incorrect because runlevel 3 produces a fully running system that permits users to access the disk. Answer C is incorrect because runlevel 4 is not normally assigned, so assuming it's a maintenance runlevel is not reliable.

- 8. Answer D is correct because LILO is installed by default in the master boot record. Answer A is incorrect because the **map** file is used to store system information for LILO's use. Answer B is incorrect because the first sector of the partition is a valid installation target, but it's not the default. Answer C is incorrect because the **boot.b** file is used to store the binary code that LILO writes, but not the bootstrap code.

- 9. Answer B is correct because the older versions of Linux used the **inetd** super server to provide on-demand services, not the **xinetd** daemon. Answer A is incorrect because the **services** file is where ports are mapped to services, but it does not provide those services on demand. Answer C is incorrect because it is the **xinetd** daemon's top-level configuration file. Answer D is incorrect because the **/etc/sysconfig** directory is not a file.

- 10. Answer: **init 3** (An alternative answer is **telinit 3**.)

- 11. Answer: **init q** (There are no alternative correct answers.)

- 12. Answer D is correct because only the **lprm** command by itself deletes just the current job from the default queue. Answer A is incorrect because **lprm -a** deletes the current job from all configured queues. Answer B is incorrect because **lprm all** deletes all the print jobs from the default queue. Answer C is incorrect because there is no way to specify the default with the **-P** option; it requires a printer name.

- 13. Answers A and E are correct because they both print three copies of the **codesamp** file. Answer B is incorrect because the **-c** option is for printer classes, not copies. Answer C is incorrect because there isn't a **-count** option for **lpr**. Answer D is incorrect because there isn't a **--copies** option for **lpr**.

- 14. Answer: **/etc/hosts.lpd** (There are no alternative correct answers.)

- 15. Answer A is correct because the **/usr/sbin/makedbwhatis** command creates the shared **whatis** database that's used by both the **whatis** and **apropos** commands. Answer B is incorrect because there isn't a **makedbapropos** command. Answer C is incorrect because, although a **makeinfo** command does exist, it's for making **Texinfo** files. Answer D is incorrect because there isn't a **makeman** command.

- 16. Answer C is correct because the **whatis** command searches for the requested command and returns a single line per found result, including a description. Answer A is incorrect because the **man** command doesn't show a single line; it shows the **man** page for the command. Answer B is incorrect because **apropos** shows many lines all containing the command's name, not just a single line for the command. Answer D is incorrect because the **whereis** command shows the binary, source, and **man** page locations, but not a description.

- 17. Answers A and D are correct because they both show any instances in the **whatis** database for the command name you're searching for. Answer B is incorrect because **man -a** can potentially show multiple pages of output, but only if there are multiple hits for the search, and then only on a page-by-page basis. Answer C is incorrect because **whatis** shows only the **man** pages that match the command name, not as a keyword. Answer E is incorrect because **whereis** shows the binary, source, and **man** page locations, but rarely more than one line's worth.

- 18. Answer: **man 5 crontab** (There are no alternative correct answers.)

- 19. Answer: **man -a tarfoo** (There are no alternative correct answers.)

- 20. Answer: **www.tldp.org** (There are no alternative correct answers.)

- 21. Answer: **declare -F** (There are no alternative correct answers.)

- 22. Answer: **/etc/nologin** (There are no alternative correct answers.)

- 23. Answer C is correct because, when a script is run, a shell is used. Any variables defined in that shell are removed when the shell is exited, even if it's exported. Answers A, B, and D are incorrect because the shell's variables are removed upon exit.

- 24. Answer A is correct because **cron** doesn't store the environment of the user running the script but **at** does. Answer B is incorrect because setting the user to be **root** does not fix the path problem. Answer C is incorrect because there is no way to export the user's environment in **cron**; you should use **cron** to invoke an **at** job. Answer D is incorrect because moving the script's location does not solve the problem.

- 25. Answer D is correct because only a Telnet user signing on is shown the contents of the **/etc/issue.net** file. All other answers are incorrect because only Telnet users are shown the **/etc/issue.net** file.

- 26. Answer C is correct because a function runs its commands in the current shell. Answer A is incorrect because an alias doesn't allow arguments or requests for input--only a function does. Answer B is incorrect because the **.inputrc** file is for defining the default key bindings, among other things. Answer D is incorrect because a script is run in a shell.

- 27. Answer C is correct because the /usr directory tree is often mounted from another system or shared out to other systems, in the case of a server. Unless an application or set of system files is changed, the /usr partition is relatively stable. Answer A is incorrect because every time you add, remove, or modify any of your configuration, the /etc directory contents are changed. Answer B is incorrect because the /home directory and tree is often on its own partition and should be backed up nightly if you have any user data changes. Answer D is incorrect because the data in /var includes log files, Web sites, and FTP sites, and print spools—all of which change often.

- 28. Answers A and B are correct because they both set the maximum number of days since the password was changed that it can be valid. Answer C is incorrect because the option needs to be a -, not a +. Answer D is incorrect because the useradd -e option is for an exact expiration date, not the number of days that a password is considered valid. Answer E is incorrect because the usermod -f option sets the number of inactive days, not the maximum number of valid days for the password.

- 29. Answer D is correct because the pwconv utility is used to move the encrypted passwords from the /etc/passwd file to the /etc/shadow file and replace them with an x in the password field. Answer A is incorrect because there isn't a passwconv command on a Linux box by default. Answer B is incorrect because there isn't a pwconvert command on a Linux box by default. Answer C is incorrect because the passwd program doesn't have a -conv option. Answer E is incorrect because the passwd command doesn't have a -mx5 option.

- 30. Answer D is correct because the correct location is /etc/default/useradd, which is a file. Answer A is incorrect because it's default, not defaults. Answer B is incorrect because there isn't a file on a standard Linux system named /etc/sysconfig/useradd. Answer C is incorrect because there isn't a file on a standard Linux system named /etc/useradd. Answer E is incorrect because the /etc/login.defs file is for site-specific configuration for the shadow suite.

- 31. Answer C is correct because the ~/.bash_logout file is read after the user initiates a sign-out via exit, logout, or Ctrl+D and typically includes the single command clear to clear the screen. All other answers are incorrect because they are used to set up the user's environment and shell, whereas the .bash_logout file is always the last file to be read or sourced in the session.

- 32. Answer: `*/20 8-18 * * 1-5 script1` An alternative answer is `0,20,40 8-18 * * Mon-Fri script1`.

- 33. Answer C is correct because /etc/cron.allow is where you put usernames that are allowed to use the cron daemon to submit jobs. All other answers are nonexistant files on a standard Linux system.
