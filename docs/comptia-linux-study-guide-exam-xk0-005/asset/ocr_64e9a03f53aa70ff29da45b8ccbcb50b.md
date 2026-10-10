These settings apply to the length and age of a password but not to the complexity level. For that, you need to use features in the pluggable authentication modules (PAM) authentication services (see Chapter 16, “Looking at Access and Authentication Methods”).

As mentioned in Chapter 16, the PAM system provides libraries that control how the Linux system authenticates user accounts for access. Each library uses settings that customize the method and process used to authenticate users. Defining password complexity rules is one of those library settings.

The *pquality.so* library defines password rules that apply to the system user accounts. By adding this library to the PAM rules, you can set additional password rules above what the standard */etc/login.defs* settings define.

> NOTE
> 
> The *pquality.so* library is installed by default in Red Hat-based distributions, but you must install it in Debian-based distributions.
> For Debian-based distributions, such as Ubuntu, install the `libpam-pwquality` software package.

In Red Hat-based distributions, you define the password quality settings in the */etc/pam.d/system-auth* configuration file. For Debian-based distributions, you define them in the */etc/pam.d/common-password* file. In both files the quality settings are defined on this line:

```
password requisite pam_pwquality.so
```

The settings are added at the end of the line, in this format:

```
*directive=value*
```

Table 19.1 shows the standard password directives available in the *pquality.so* library.

# TABLE 19.1  PAM password standard directives

| Directive | Description |
| :--- | :--- |
| *difok* | Specifies the number of character changes in a new password from the old password |
| *enforce_for_root* | Specifies if the password enforcement rules apply to the root user account |
| *maxrepeat* | Specifies the maximum number of characters that can repeat |
| *minlen* | Specifies the minimum password length |
| *reject_username* | Rejects a password if it contains the username spelled either forward or in reverse |
| *retry* | Specifies the number of password attempts that are allowed |