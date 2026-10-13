# CERTIFICATION OBJECTIVE 8.02

# Administrative Control

As the root administrative user is all-powerful, it's important for administrators to execute most actions as the regular user. Limits on regular users can help protect Linux systems from accidents. Regular users who have the root administrative password can temporarily take root privileges with the su command. The su command can do more with other accounts. In contrast, the sg command is associated with privileges on special groups.

While the su command is adequate for small networks, no administrator should work alone. With the help of the sudo command configured in the /etc/sudoers file, it's possible to set up dedicated administrators with partial or complete root administrative privileges.

# The Ability to Log In as root

It's possible to keep users from logging in directly as the root administrative user. Local access is regulated in the /etc/securetty file. By default, it contains access directives for 12 virtual consoles. While only six virtual consoles are enabled in the /etc/init/start-ttys.conf file discussed in Chapter 5, it is possible to configure 12 (based on the number of function keys on a keyboard).

The virtual consoles listed in /etc/securetty determine the consoles where the root administrative user is allowed to log in. If the directives in this file were commented out, administrators would not be able to log in directly to the root account. They'd have to log in to a regular account and use either the su or sudo command for administration.

While it's still possible to log in remotely as the root administrative user with the ssh command, that ability can also be regulated. The configuration of the SSH server in this manner is an RHCE skill described in Chapter 12.

# EXERCISE 8-3

# Limit root Logins

In this exercise, you'll examine the effect of eliminating the consoles in the /etc/securetty file. But first, you'll confirm that the root administrative user can log