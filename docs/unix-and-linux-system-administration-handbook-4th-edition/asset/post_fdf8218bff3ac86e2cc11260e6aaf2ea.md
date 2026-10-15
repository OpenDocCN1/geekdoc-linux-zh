
## 7.8 DISABLING LOGINS

On occasion, a user's login must be temporarily disabled. A straightforward way to do this is to put a star or some other character in front of the user's encrypted password in the /etc/security/passwd (AIX) or /etc/shadow file. This measure prevents most types of password-regulated access because the password no longer decrypts to anything sensible. Commands such as ssh that do not necessarily check the system password may continue to function, however.

On all our Linux distributions, the usermod -L user and usermod -U user commands provide an easy way to lock and unlock passwords. They are just shortcuts for the password twiddling described above: the -L puts an ! in front of the encrypted password in the /etc/shadow file, and the -U removes it.

Root on Solaris can lock an account with passwd -l loginname, force a user to change his or her password with the -f flag, or unlock the account with -u. Locking an account adds \*LK\* to the password field of /etc/shadow. This is also the value set by useradd for new users.

HP-UX supports only crypt-encoded passwords. The * character can never belong to a crypt-generated password field, so adding a * to the encrypted password prevents the user from logging in.

On AIX, if the password placeholder field of /etc/passwd contains a * instead of an !, the account is locked. AIX's pwdadm command can force a user to change his or her password, or it can lock the account so that only an administrator can change the password.

Unfortunately, modifying a user's password simply makes logins fail. It does not notify the user of the account suspension or explain why the account no longer works. An alternative way to disable logins is to replace the user's shell with a program that prints an explanatory message and supplies instructions for rectifying the situation. The program then exits, terminating the login session.

This approach has both advantages and disadvantages. Any forms of access that check the password but do not pay attention to the shell will not be disabled. To facilitate the "disabled shell" trick, many daemons that provide nonlogin access to the system (e.g., ftpd) check to see if a user's login shell is listed in /etc/shells and deny access if it is not. This is the behavior you want. Unfortunately, it's not universal, so you may have to do some fairly comprehensive testing if you decide to use shell modification as a way of disabling accounts.

Another issue is that your carefully written explanation of the suspended account might never be seen if the user tries to log in through a window system or through a terminal emulator that does not leave output visible after a logout.

By default, sendmail will not deliver mail to a user whose shell does not appear in /etc/shells. It's a bad idea to interfere with the flow of mail, even if the recipient is not able to read it immediately. You can defeat sendmail's default behavior by adding a fake shell named /SENDMAIL/ANY/SHELL/ to the /etc/shells file.

## 7.9 MANAGING USERS WITH SYSTEM-SPECIFIC TOOLS

HP-UX and AIX provide a comprehensive system administration tool that knows how to manage users, at least in a rudimentary fashion. In AIX it's SMIT, the System Management Interface Tool, and in HP-UX it's now called smh, the System Management Homepage. (It was called sam, the System Administration Manager, in earlier HP-UX releases.) Each of these tools has screens for adding and managing users, either with a windows-based GUI or with a terminal interface based on the curses library. If you are a brand new sysadmin or an old hand on a new and different operating system, these tools are a reasonable place to start for many of the common sysadmin tasks.

AIX's smitty has a handy feature: if you hit F6, it shows you the command and arguments that it is planning to execute. It also logs all interactions and keeps a script file of the commands it executed on your behalf. This can be a good learning tool as you become familiar with AIX's quirks. HP-UX's smh has nice single-character shortcuts for its curses interface. They are shown on each menu page so you can quickly get to the command you need.

## 7.10 REDUCING RISK WITH PAM

Pluggable Authentication Modules (PAM) are covered in the Security chapter starting on page 908. They centralize the management of the system's authentication facilities through standard library routines so that programs like login, sudo, passwd, and su do not have to supply their own tricky authentication code. PAM reduces the risk inherent in writing secured software, allows administrators to set site-wide security policies, and defines an easy way to add new authentication methods to the system.

Adding and removing users doesn't involve twiddling the PAM configuration, but the tools involved operate under PAM's rules and constraints. In addition, many of the PAM configuration parameters are similar to those used by useradd or usermod. If you change a parameter as described in this chapter and useradd doesn't seem to be paying attention to it, check to see if the system's PAM configuration is overriding your new value.

## 7.11 CENTRALIZING ACCOUNT MANAGEMENT

Some form of centralized account management is essential for medium-to-large enterprises of all types, be they corporate, academic, or governmental. Users need the convenience and security of a single login name, UID, and password across the site. Administrators need a centralized system that allows changes (such as account revocations) to be instantly propagated everywhere.
