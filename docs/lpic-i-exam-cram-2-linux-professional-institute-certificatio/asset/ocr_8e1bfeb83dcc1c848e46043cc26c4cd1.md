6. Which command is used to set the password expiration, warning, and other `/etc/shadow` file field information interactively?

O A. **passwd**
O B. **chpass**
O C. **vipw**
O D. **chage**

Answer D is correct because using the `chage username` command *interactively* asks and sets the `/etc/shadow` options. Answer A is incorrect because the `passwd` command doesn't interactively change the options in the `/etc/shadow` file. Answer B is incorrect because there is no such thing as a `chpass` command. Answer C is incorrect because the `vipw` command is used to alter the `/etc/passwd` file.

7. If you see a **passwd** file that apparently contains some encrypted passwords and what appear to be x shadow password indicators in the second field, which command would you use to attempt to fix this?

O A. **chown**
O B. **pwconv**
O C. **pwck**
O D. **chfn**

Answer B is correct because `pwconv` is used to convert `passwd` files to shadow files. Answer A is incorrect because the `chown` command is used to change ownership of objects. Answer C is incorrect because the `pwck` file checks the validity of the user accounts but does not convert them to shadow entries. Answer D is incorrect because `chfn` changes the finger-related information and has nothing to do with the encrypted passwords.

8. Which command enables a user to alter her primary group until they log out? Fill in the blank below with just the name of the command:

________________________________

The correct answer is `newgrp`. There are no alternative answers.

9. What are the default permissions for the Debian and Red Hat `/etc/passwd` files? Fill in the blank below with the three numerals that represent the octal value for the permissions:

________________________________

The correct answer is 644. There are no alternative answers.

10. Which command shows the user which settings are in place for the maximum allowable size of files created in the shell, if configured?

O A. **umask**
O B. **dmesg**
O C. **ulimit**
O D. **perms**