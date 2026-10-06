stack. PAM calls the modules one at a time in order, from the top of the stack (the
first module listed in the configuration file) to the bottom of the stack. The modules
report success or failure back to PAM. When all (there are exceptions) the stacks of
modules within a configuration file have been called, the PAM library reports suc-
cess or failure back to the application.

# Example

Part of the login service's authentication stack follows as an example:

```
$ cat /etc/pam.d/login
%PAM-1.0
auth required      /lib/security/pam_security.so
auth required      /lib/security/pam_stack.so service=system-auth
auth required      /lib/security/pam_nlogin.so
```

The login program first asks for a user name and then asks PAM to run this stack to
authenticate the user. Refer to the Table 17-19 on page 1045 and Table 17-20 on
page 1046.

+   1. PAM first calls the pam_security (secure tty) module to make sure that the
root user logs in only from an allowed terminal (by default, root is not
allowed to log in over the network; this policy prevents security
braches). The pam_security module is required to succeed in order for
the authentication stack to succeed. The pam_security module reports
failure only if someone is trying to log in as root from an unauthorized
terminal. Otherwise (if the user name being authenticated is not root or if
t user name is root and the login attempt is being made from a secure
terminal), the pam_security module reports success.

Success and failure within PAM are opaque concepts that apply only to
PAM. They do not equate to true and false as used elsewhere in the
operating system.

+   2. The pam_stack.so module diverts the PAM stack to another module,
returning the success or failure as the other module returns to it. The
service=system-auth gives the name of the other module, in this case
system-auth in /etc/pam.d. This module checks that the user who is
logging in is authorized to do so, including checks the username and
password.

+   3. Next, the pam_nlogin module makes sure if the /etc/nlogin.txt file
exists, only the root user is allowed to log in. (That is, the pam_nlogin
module reports success only if /etc/nlogin.txt does not exist or if the root