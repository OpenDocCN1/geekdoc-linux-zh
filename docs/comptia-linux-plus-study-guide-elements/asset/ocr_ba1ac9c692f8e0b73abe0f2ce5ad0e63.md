Verifying that an account exists is the first step in authentication. The second step is to check the password that the user types using an authentication tool. In Linux, this task is handled via PAM. The idea behind PAM is that every tool that requires authentication has its own needs and so can be configured individually. This is done via files in `/etc/pam.d`, as described in “Configuring PAM.” PAM enables you to set up different rules for authenticating users for each login method—local text-mode console logins, local GUI console logins, remote logins via SSH, e-mail retrieval via POP or IMAP, and so on. This feature can be useful because you can set different conditions and actions. For instance, you might want to ensure that users have valid home directories for console or remote text-mode or GUI logins, but this requirement may not be important for users who only retrieve e-mail via a POP mail server.

# ## Configuring PAM

Unfortunately, PAM configurations vary substantially from one distribution to another. Typically, `/etc/pam.d` contains a large number of files, most of which are named after particular servers or other login tools, such as `gdm`, `login`, `passwd`, `sshd`, and `su`. (Very old distributions used the `/etc/pam.conf` file to configure PAM, but this style of PAM configuration has long since gone the way of the dodo.) To better understand PAM, consider a typical PAM configuration file, from `/etc/pam.d/login` on a Fedora system, shown in Listing 12.1.

# **Listing 12.1: A Typical PAM Configuration File**

```
```text
#%PAM-1.0
auth [user_unknown=ignore success=ok ignore=ignore default=bad]
    pam_securityt.so
auth    include    system-auth
account    required    pam_nologin.so
account    include    system-auth
password    include    system-auth
# pam_selinux.so close should be the first session rule
session    required    pam_selinux.so close
session    required    pam_loginuid.so
session    optional    pam_console.so
# pam_selinux.so open should only be followed by sessions to be executed
# in the user context
session    required    pam_selinux.so open
session    required    pam_namespace.so
session    optional    pam_keyinit.so force revoke
session    include    system-auth
session    optional    pam_ck_connector.so
```
```