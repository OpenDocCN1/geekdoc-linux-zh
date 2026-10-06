# Chapter 10: Understanding System Administration 421

> TIP: Because most Fedora and RHEL administrative features are expected to be administered by the root user, e-mail for other administrative accounts is routed to the root user. If you want other administrative users to receive their own e-mail, delete the aliases for those users from the /etc/aliases file.

# Understanding administrative logins

Here are some of the administrative logins that are configured automatically for Linux systems. By tradition, these logins are assigned UID numbers up to 100. Here are examples:

> TIP: Most administrative logins have no passwords by default. They also typically have /sbin/nologin assigned as them, so if you try to log in as one of these users, you see This account is currently not available message. That's why you can't use an administrative login until you assign it a password and shell (such as /bin/bash).

+   - This user can control printing features. Having a separate lp administrator allows someone other than the super user to do things like remove lp logs and print spool files. The home directory for lp is /var/spool/lp
- This user can work with administrative e-mail features. The mail group has permissions to use mail files in /var/spool/mail (which is also the mail user's home directory).
- uucp This user owns various most commands (used as the primary method for dial-serial communications). It is the owner of log files in /var/log/uucp, spool files in /var/spool, administrative commands (such as uucch, uuico, uconv, and uuqt) in /usr/bin. The home directory for uucp is /var/spool/uucp.
- bin This user has many commands in /bin in traditional UNIX systems. This is not the case in Fedora and RHEL root tends to own most executable files. The home directory of bin is /bin
- news This user could do administration of Internet news services, depending on how you set permission for /var/spool/news and other news-related resources. The directory for news is /etc/news.

# Using sudo for administrative privilege

One way to get full or limited privileges to any non-root user is to set up the sudo facility. That simply adding the user to /etc/sudoers and defining what privilege you want that user to have. The user can run any command he or she is privileged to by preceding that command with the sudo command.

The following is an example of how to use the sudo facility to access any users that are added to the wheel group to have root privileges:

+   1. As the root user