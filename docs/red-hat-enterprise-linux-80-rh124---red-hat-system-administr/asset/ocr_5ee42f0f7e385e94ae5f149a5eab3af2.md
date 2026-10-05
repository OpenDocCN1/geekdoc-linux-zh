# GAINING SUPERUSER ACCESS

# OBJECTIVES

After completing this section, you will be able to switch to the superuser account to manage a Linux system, and grant other users superuser access through the sudo command.

# THE SUPERUSER

Most operating systems have some sort of superuser, a user that has all power over the system. In Red Hat Linux this is the root user. This user has the power to override normal privileges on the file system, and is used to manage and administer the system. To perform tasks such as installing or removing software and to manage system files and directories, users must escalate their privileges to the root user.

The root user only among normal users can control removable devices, but there are a few exceptions. For example, normal users can control removable devices, such as USB devices. Thus, normal users can add and remove files and otherwise manage a removable device, but only root can manage "fixed" drives by default.

This unlimited privilege, however, comes with responsibility. The root user has unlimited power to damage the system: remove files and directories, remove user accounts, add back doors, and so. If the root user's account is compromised, else would have administrative control of the system. Throughout this course, administrators are encouraged to log in as a normal user and escalate privileges to root only when needed.

The root account on Linux is roughly equivalent to the local Administrator account on Microsoft Windows. In Linux, most administrators log in to the system as an unprivileged user and use various tools to temporarily gain root privileges.

> One common practice in Microsoft Windows in the past was for the local Administrator to log in to perform system administrator duties. Although this is possible on Linux, Red Hat recommends that administrators not log in directly as root. Instead, system administrators should log in as a normal user and use other mechanisms (su, sudo, or PolicyKit, for example) to temporarily gain superuser privileges.

By logging in as the superuser, the entire desktop environment unnecessarily with administrative privileges. In that situation, any security vulnerability which would normally compromise the user account has the potential to compromise the entire system.

# SWITCHING USERS

The su command allows users to switch to a different user account. If you run su from a regular user account, you will be prompted for the password of the account to which you want to switch. When root runs su, no need to enter the password.