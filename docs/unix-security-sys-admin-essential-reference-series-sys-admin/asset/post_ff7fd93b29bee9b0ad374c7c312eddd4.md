
## Log In as root

This process can be done either while logged in directly as root from the system console or while logged in from a terminal or across the network as a regular, non-privileged user su ed to root. Check that Enhanced Security is not already enabled with the following command.

```
# /usr/sbin/rcmgr get SECURITY
```

If the string BASE is returned, you are running Base Security. If, however, the string ENHANCED is returned, Enhanced Security is already enabled on this system, and you should jump to Step 5 (the section "Adjust System Default Database") to adjust the global defaults.

## System Default Database File Format — continued

d_pw_expire_warning This option, in seconds, is used to determine whether a password expiration warning is given at login time. If the password expiration for a user falls within this time interval, a warning is given.

d_pw_site_callout This option specifies the full pathname of the script to call for site-specific security policy conformance decisions. The /etc/bin/pwpolicy by default does nothing but exit with a positive return code. See the "DEC OSF/1 Security" manual for more information on this option.

u_minchg#0 This option specifies the minimum time between password changes in seconds. If the value assigned is zero (0), there is no minimum time enforced.

u_minlen#8 This option specifies the minimum password length.

u_maxlen#12 This option specifies the maximum password length.

u_exp#0 This option specifies the number of seconds after a successful password change that the account password will expire. If the values specified is zero (0), passwords will not expire.

## Install the Enhanced Security Subsets

Before you can enable Enhanced Security, two Enhanced Security Software Subsets must be loaded. These subsets are named OSF C2SECxxx and OSF XC2SECxxx. (The xxx specifies the version of the subset.) To determine whether these subsets are loaded, you can check as shown by the following command and output.

```
# /usr/sbin/setld -i | grep -i c2sec
OSFC2SEC350 installed C2-Security (System Administration)
OSFXC2SEC350 installed C2-Security GUI (System Administration)
```

In this example, both subsets are installed. If you do not receive any output or if the installed keyword is absent, you must install both subsets from the master operating system install media using the setld command. For assistance, see the "Installation Guide" for your revision of the operating system.

## System Default Database File Format — continued

u_pwdepth#0 This option specifies the number of old encrypted passwords to save to prevent reuse. A value of zero (0) indicates that old passwords can be reused.

u_nullpw@ This Boolean option controls the ability of a user to choose a null password. A u_nullpw entry indicates a null password can be chosen; a u_nullpw@ indicates that it cannot.

u_genchars@ This Boolean option controls the ability of a user to generate random characters for a password. A u_genchars entry indicates that the user can generate passwords made up of random characters; a u_genchars@ entry indicates that she cannot.

u_genletters@ This Boolean option controls the ability of a user to generate random letters for a password. A u_genletters entry indicates that the user can generate passwords made up of random letters; a u_genletters@ entry indicates that he cannot.

u_maxtries#0 This option specifies the maximum number of consecutive unsuccessful login attempts to an account before the account is locked. Setting this option to zero (0) disables the locking of accounts due to unsuccessful login attempts.

u_lock@ This Boolean option is used to administratively lock an account. A u_lock entry indicates that the account is locked; a u_lock@ entry indicates that it is not. The presence of the u_lock@ entry in the Default Database File is to globally indicate that all accounts are unlocked unless locked in the individual Protected Password Database Files.

t_logdelay#2 This option specifies the number of seconds between unsuccessful login attempts. This field is designed to slow the rate at which login attempts on a terminal device can occur.

t_maxtries#10 This option specifies the maximum number of consecutive unsuccessful login attempts permitted using the terminal before the terminal is locked. Once the terminal is locked, it must be unlocked by an authorized administrator. For additional information, see the manpage for default(4).
