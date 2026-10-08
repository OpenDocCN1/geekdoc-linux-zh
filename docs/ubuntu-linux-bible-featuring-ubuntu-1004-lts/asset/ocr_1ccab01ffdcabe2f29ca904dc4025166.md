# Chapter 27: Managing Users, Groups, and Authentication

application uses PAMs and you forget to create its PAM configuration file or that file is somehow accidentally deleted? To cover these cases, the Linux-PAM library provides a default configuration file for any applications and services that do not have their own configuration files. This is the file /etc/pam.d/other, which has the following valid entries on a standard Ubuntu system:

```
@include common-auth
@include common-account
@include common-password
@include common-session
```

The contents of each of these files was discussed earlier in this chapter, the section entitled "Example: PAMs Used by the Login Process." On Ubuntu systems, by default, the /etc/pam.d/other PAM configuration file provides a reasonable set of defaults for verifying that random are at least executed by someone who can successfully log in and authenticate himself or herself to the system, and guarantees that various log entries for that user are created.

# Tip

Because a misconfigured PAM configuration file generally indicates a misconfigured system or that someone has imported a PAM-aware binary without thinking through you, you can use the /etc/pam.d/other file to disable access and impose extreme paranoid security, by changing it to the following entries:

```
auth required pam_deny.so
auth required pam_warn.so
account required pam_deny.so
account required pam_warn.so
password required pam_deny.so
password required pam_warn.so
session required pam_deny.so
session required pam_warn.so
```

Because subsequent required entries for a module type are all executed, each module-type entry first executes the pam_deny.so PAM, which denies access to the requested service, and then executes the pam_warn.so PAM, which enters a warning message to the system log. These log entries will help you identify the problem if a crank user hasn't already searched and asked why they can no longer run some obscure binary that they imported. ■

# Customizing the sudo Command

As introduced in the section of Chapter 4 entitled "Performing Privileged Operations," Ubuntu does not use the traditional root account to perform privileged operations but instead needs users who are members of the admin group to perform all privileged operations by specifying their own passwords. The rationale for the root account (and its traditional friend, the sudo command) are disabled on these systems is discussed in the official Ubuntu documentation at https://help.ubuntu.com/community/RootSudo. To save you Web lookup, this is