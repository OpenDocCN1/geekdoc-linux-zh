# FIGURE 10-10

PAM configuration files in the /etc/pam.d directory

```
[root@server1 ~]# ls /etc/pam.d/
atd                halt                smartcard-auth-ac
authconfig         ksu                 swtp
authconfig-gtk     login               smtp.postfix
authconfig-tui     newrole             sshd
chfn               other               su
chsh               passwd              sudo
config-util        password-auth       sudo-i
crond              password-auth-ac    su-l
cups               polkit-1            system-auth
cvs                poweroff            system-auth-ac
eject              reboot              system-config-authentication
fingerprint-auth   remote              system-config-date
fingerprint-auth-ac rhn_register        system-config-kdump
gdm                run_init            system-config-keyboard
gdm-autologin      runuser             system-config-network
gdm-fingerprint    runuser-l           system-config-network-cmd
gdm-password       setup               system-config-users
gdm-smartcard      smartcard-auth      xserver
[root@server1 ~]#
```

# Control Flags

The PAM system divides the process of verifying users into four separate tasks. These are the four different types of PAM flags:

+   - **Authentication management (auth)** Establishes the identity of a user. For example, a PAM auth command decides whether to prompt for a username and/or a password. Related options may even grant group membership.
+   - **Account management (account)** Allows or denies access according to the account policies. For example, a PAM account command may deny access according to time, password expiration, or a specific list of restricted users.
+   - **Password management (password)** Manages other password policies. For example, a PAM password command may limit the number of times a user can try to log in before a console is reset.
+   - **Session management (session)** Applies settings for an application. For example, the PAM session command may set default settings for a login console.

The code shown in Figure 10-11 is from an example PAM configuration file, /etc/pam.d/login. Every line in all PAM configuration files is written in the following format:

```
module_type  control_flag  module_path  [arguments]
```