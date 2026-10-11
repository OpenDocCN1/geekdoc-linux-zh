![](bbox=[0.3, 0.08, 0.87, 0.22])

![](bbox=[0.05, 0.07, 0.2, 0.15])

This behavior is actually configured in the /etc/pam.d/login file, shown in this example:

```
```
###PAM-1.0
auth        requisite     pam_nologin.so
auth    [user_unknown=ignore success=ok ignore=ignore auth_err=die
default=bad] pam_security.so
auth        include       common-auth
account   include       common-account
password  include       common-password
session   required      pam_loginuid.so
session   include       common-session
session   required      pam_lastlog.so nowtmp
session   optional      pam_mail.so standard
session   optional      pam_ck_connector.so
```
```

The line that reads auth requisite pam_nologin.so causes PAM to check and see if a file named nologin exists in /etc. If it does, then PAM does not allow regular users to log in. When you’re done, you can re-enable logins by deleting or renaming the nologin file. For example, you could rename it to etc/nologin /etc/nologin.bak at the shell prompt.

Let’s next discuss how to audit files by locating files with the SUID or SGID permission set.

# Auditing Files

In addition to disabling user login, another user security-related issue you need to be familiar with is auditing files that have SUID root permissions set. As you learned in Chapter 11, SUID stands for Set User ID. When an executable file with the SUID permission set

![](bbox=[0.06, 0.81, 0.75, 0.88])