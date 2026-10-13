
## FIGURE 10-10

PAM configuration files in the /etc/pam.d directory

```
[root@server1 ~]# ls /etc/pam.d/
atd                halt                smartcard-auth-ac
authconfig         ksu                 sftp
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

## Control Flags

The PAM system divides the process of verifying users into four separate tasks. These are the four different types of PAM flags:

- **Authentication management (auth)** Establishes the identity of a user. For example, a PAM auth command decides whether to prompt for a username and/or a password. Related options may even grant group membership.
- **Account management (account)** Allows or denies access according to the account policies. For example, a PAM account command may deny access according to time, password expiration, or a specific list of restricted users.
- **Password management (password)** Manages other password policies. For example, a PAM password command may limit the number of times a user can try to log in before a console is reset.
- **Session management (session)** Applies settings for an application. For example, the PAM session command may set default settings for a login console.

The code shown in Figure 10-11 is from an example PAM configuration file, /etc/pam.d/login. Every line in all PAM configuration files is written in the following format:

```
module_type  control_flag  module_path  [arguments]
```

## FIGURE 10-11

The PAM /etc/pam.d/login configuration file

```
#PAM-1.0
auth [user_unknown=ignore success=ok ignore=ignore default=bad] pam_securetty.so
auth include system-auth
account required pam_nologin.so
account include system-auth
password include system-auth
# pam_selinux.so close should be the first session rule
session required pam_selinux.so close
session required pam_loginuid.so
session optional pam_console.so
# pam_selinux.so open should only be followed by sessions to be executed in the
user context
session required pam_selinux.so open
session required pam_namespace.so
session optional pam_keyinit.so force revoke
session include system-auth
-session optional pam_ck_connector.so
~
~
"/etc/pam.d/login" 16L, 728C
```

The module_type, as described previously, can be auth, account, password, or session. The control_flag determines what PAM does if the module succeeds or fails. The module_path specifies the location of the actual PAM module file. Finally, as with regular shell commands, you can specify arguments for each module.

The control_flag field requires additional explanation. It determines how the configuration file reacts when a module flags success or failure. The five different control flags are described in Table 10-5.

## TABLE 10-5

PAM Control Flags

| control_flag | Description |
|---|---|
| required | If the module works, the command proceeds. If it fails, PAM proceeds to the next command in the configuration file—but the command controlled by PAM will still fail. |
| requisite | Stops the process if the module fails. |
| sufficient | If the module works, the login or other authentication proceeds. No other commands need be processed. |
| optional | PAM ignores success or failure of this module, unless no other modules are used. |
| include | Includes all module_type directives from the noted configuration file; for example, if the directive is password include system-auth, this includes all password directives from the PAM system-auth file. |

To see how control flags work, take a look at the commands from the /etc/pam.d/reboot configuration file:

```
auth sufficient pam_rootok.so
```

The first auth command checks the pam_rootok.so module. In other words, if the root user runs the reboot command, the control_flag is sufficient, and the other auth commands in this file are ignored. Linux runs the reboot command. This is explained in the README.pam_rootok file in the /usr/share/doc/pam-versionnumber/txts directory.

```
auth required pam_console.so
```

Given the purpose of the first line, this second auth command is run only for nonroot users, to govern permissions within the console. In this case, it just confirms console ownership to any user who is logged in to that console.

```
#auth include system-auth
```

The third line is commented out by default. If you make this line active, it includes the commands from the system-auth configuration file, which requires root user privileges. Remote users who connect with root privileges are still allowed to reboot the system.

```
account required pam_permit.so
```

The module associated with the account command (pam_permit.so) accepts all users, even those who've logged in remotely. In other words, this configuration file would allow any root user, local or remote, to reboot the Linux system, unless rejected by a previous directive.

## The Format of a PAM File

This section is a little complex. It starts with the /etc/pam.d/login configuration file shown in Figure 10-12. In addition, as the file includes references to the /etc/pam.d/system-auth configuration file, you'll need to go back and forth between files to follow along with this section.

When a user opens a text console and logs in, Linux goes through this configuration file line by line. As previously noted, the first line in /etc/pam.d/login limits root user access to secure terminals as defined in the /etc/securetty file:

```
auth [user_unknown=ignore success=ok ignore=ignore default=bad] \
 pam_securetty.so
```

## FIGURE 10-12 The PAM /etc/pam.d/system-auth configuration file

```
#PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth required pam_env.so
auth sufficient pam_fprintd.so
auth sufficient pam_unix.so nullok try_first_pass
auth requisite pam_succeed_if.so uid >= 500 quiet
auth required pam_deny.so

account required pam_unix.so
account sufficient pam_localuser.so
account sufficient pam_succeed_if.so uid < 500 quiet
account required pam_permit.so

password requisite pam_cracklib.so try_first_pass retry=3 type=
password sufficient pam_unix.so sha512 shadow nullok try_first_pass use_authtok
password required pam_deny.so

session optional pam_keyinit.so revoke
session required pam_limits.so
session [success=1 default=ignore] pam_succeed_if.so service in crond quiet
use_uid
session required pam_unix.so
~
"/etc/pam.d/system-auth" 22L, 937C
```

The next line includes the auth commands from the system-auth PAM configuration file:

```
auth include system-auth
```

The system-auth configuration file shown in Figure 10-12 includes five auth directives:

```
auth required pam_env.so
auth sufficient pam_fprintd.so
auth sufficient pam_unix.so nullok try_first_pass
auth requisite pam_succeed_if.so uid >= 500 quiet
auth required pam_deny.so
```

In order, they set up environment variables, check authentication via a fingerprint reader (pam_fprintd.so) if available, and check passwords (pam_unix.so). The sufficient flag associated with those modules means that authentication works if a valid fingerprint or password has been entered. The User ID of the account must be 500 and above. If these conditions are not met, the user is locked out (pam_deny.so).

> **exam watch**
> 
> *If the /etc/nologin file exists, regular users are not allowed to log in to the local console. Any regular user that tries to log in gets to read the contents of /etc/nologin as a message.*

Now return to the /etc/pam.d/login file. The next line, which looks for an account module type, checks for accounts not allowed to log in as listed in the /etc/nologin file:

```
account required pam_nologin.so
```

The following account module includes the account modules from the /etc/pam.d/system-auth configuration file:

```
account include system-auth
```

These are the account module type lines from /etc/pam.d/system-auth:

```
account required pam_unix.so
account sufficient pam_localuser.so
account sufficient pam_succeed_if.so uid < 500 quiet
account required pam_permit.so
```

The first line refers to the pam_unix.so module in the /lib/security directory, which brings up the normal username and password prompts. Based on the pam_localuser.so module, users found in /etc/passwd are automatically accepted. Based on the pam_succeed_if.so module, service users (with user IDs less than 500) are automatically logged in, without messages (quiet). The pam_permit.so module always returns success.

Now return to the /etc/pam.d/login file. The next line is a password module, which includes other password module type lines from the /etc/pam.d/system-auth file:

```
password include system-auth
```

These are the password module type lines from /etc/pam.d/system-auth:

```
password requisite pam_cracklib.so try_first_pass retry=3
password sufficient pam_unix.so sha512 shadow nullok try_first_pass \
use_authtok
password required pam_deny.so
```

The first command from this list allows the use of a previously successful password (try_first_pass) and then sets a maximum of three retries. The next command encrypts passwords using the SHA512 hash, supports the Shadow Password Suite
