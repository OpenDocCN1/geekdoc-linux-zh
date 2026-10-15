employers used to take the cover sheet from an employee's personnel file (which contained the usual personal information of name, address, birth date, and so on) and then attempt to log on to a terminal with passwords constructed from that information—and often succeeded in logging on.

On the other hand, a password such as 2a56u`F{$8A4u#*HjU441k$%({#EJD is sure to present great difficulty to an intruder (or an auditor). However, that password is so difficult to remember that it would be likely that the password owner would write that password down and tape it next to her keyboard. I worked for a company in which the entry code to one of the buildings was etched into the cigarette bin outside the door; we never found out who did this, but quickly changed the security number. This is but one of many examples of poor security in the field.

The sysadmin has control, with settings in the /etc/shadow file, over how often the password must be changed. The settings can be changed using a text editor, the change command, or a configuration tool such as Ubuntu's User Manager, as shown previously in Figure 10.1. Click on the Password Info tab under that particular user's Properties to set individual password policies.

# Changing Passwords in a Batch

On a large system, there might be times when a large number of users and their passwords need some attention. The super user can change passwords in a batch by using the chpasswd command, which accepts input as a name/password pair per line in the following form:

```
$ sudo chpasswd username:password
```

Passwords can be changed en masse by redirecting a list of name and password pairs to the command. An appropriate shell script can be constructed with the information gleaned from Chapter 11.

However, Ubuntu also provides the newusers command to add users in a batch from a text file. This command also allows a user to be added to a group, and a new directory can be added for the user, too.

# Granting System Administrator Privileges to Regular Users

On occasion, it is necessary for regular users to run a command as if they were the root user. They usually do not need these powers, but they might on occasion—for example, to temporarily access certain devices or run a command for testing purposes.

There are two ways to run commands with root privileges: The first is useful if you are the super user and the user; the second if you are not the regular user (as on a large, multiuser network).