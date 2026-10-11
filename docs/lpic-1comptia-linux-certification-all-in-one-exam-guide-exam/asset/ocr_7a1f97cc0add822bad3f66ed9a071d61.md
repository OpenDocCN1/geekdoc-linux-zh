# LPIC-1/CompTIA Linux+ Certification All-in-One Exam Guide

696

consider implementing screen-saver passwords. You should also train your users to lock their workstations or log out completely before leaving their systems. To facilitate this, users can use the nohup command to load processes. This will allow the processes to continue running even if the user logs out from the shell prompt.

I then discussed user access controls you can use to constrain what users can and can’t do in the system. Users, groups, and permissions are the main means of controlling access to the system. However, there are other things you can do to increase the security of the system. First of all, you need to use your root user account judiciously. The root user should be used only to complete root tasks. All other tasks should be completed using a standard user account. The system should never be left unattended while the root user is logged in. You can use the su command to switch to the root user account when you need to complete tasks that require root-level access. You can use the exit command to switch back to your regular user account when done.

If you have users who occasionally need to run commands as root but you don’t want to give them your root password, you can use the sudo command. You use the /etc/sudoers file to specify which users can run which commands as root. You edit this file using the visudo utility. This utility will load the /etc/sudoers file in the vi editor. When you exit vi, it will check your syntax to make sure you didn’t make syntax errors in the file.

Next, I talked about implementing a strong password policy. Users need to be trained to avoid using passwords that can be easily guessed, such as spouses’ names, children’s names, or pets’ names. Users need to be trained to use strong passwords, which use

+   - Six or more characters
+   - Numbers in addition to letters
+   - Upper- and lowercase letters
+   - Words not found in the dictionary

You should also configure password aging with the chage command. You can specify the minimum number of days between password changes, the maximum number of days between password changes, and the number of warning days before a password change is required.

You should also verify that your Linux systems use shadow passwords. Storing passwords in /etc/passwd is highly insecure. You can use the pwconv command to migrate passwords from /etc/passwd to /etc/shadow.

In addition, you need to train your users to follow proper security procedures. You should not allow them to write their passwords down. You should also train them how to handle social engineering attempts. Users should also shred important documents rather than just throw them in the common trash.

We then looked at configuring user limits. You can impose limits on how many times users may log in, how much CPU time they can consume, and how much memory they can use on a Linux system. One way to do this is to use the pam_limits module with the Pluggable Authentication Modules (PAM) system. Limits are configured in the /etc/security/limits.conf file using the following syntax:

```
domain type item value
```