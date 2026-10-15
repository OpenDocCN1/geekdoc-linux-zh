![](bbox=[0.07, 0.12, 0.78, 0.38])

FIGURE 14.2 Adding a new user is simple. The GUI provides a more complete set of commands for user management than for group management.

NOTE
A Linux username can be any alphanumeric combination that does not begin with a special character reserved for shell script use (see Chapter 15 for disallowed characters, mostly punctuation characters). In Chapter 5, we told you that usernames are typically the user's first name plus the first initial of her last name. That is a common practice on larger systems with many users because it makes life simpler for the sysadmin, but is neither a rule nor a requirement.

# Monitoring User Activity on the System

Monitoring user activity is part of the sysadmin's duties and an essential task in tracking how system resources are being used. The w command tells the sysadmin who is logged in, where he is logged in, and what he is doing. No one can hide from the super user. The w command can be followed by a specific user's name to show only that user.

The ac command provides information about the total connect time of a user measured in hours. It accesses the /var/log/wtmp file for the source of its information. The ac command proves most useful in shell scripts to generate reports on operating system usage for management review. Note that you have to install the acct package using either synaptic or apt-get