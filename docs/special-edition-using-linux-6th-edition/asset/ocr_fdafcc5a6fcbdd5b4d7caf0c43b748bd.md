> **Caution:** The order of lines is important where requisite and sufficient controls are concerned; otherwise, order is unimportant. Always test authentication scenarios when making changes to the PAM authentication files.

The third column specifies the particular module to use. Modules are installed by default in `/lib/security`. To properly use modules, you’ll need to understand them. This text discusses some of the more common modules in the next section. These modules change from upgrade to upgrade, normally with more being added, so this text cannot be the authoritative source for the modules. That must be left to the READMEs installed in `/usr/doc/libpam-<version>/`.

The fourth column contains any options you want to assign to the module. The READMEs for the modules contain a list of the valid options available for each module. These options can also change from upgrade to upgrade, so the READMEs should be consulted.

# UNDERSTANDING THE MODULES

The following is a list of modules installed in earlier versions of OpenLinux (2.4 and earlier):

+   - `pam_access.so`  | `pam_cracklib.so`   | `pam_deny.so`
+   - `pam_dialup.so`   | `pam_env.so`        | `pam_ftp.so`
+   - `pam_group.so`    | `pam_lastlog.so`    | `pam_ldap.so*`
+   - `pam_limits.so`   | `pam_lastfile.so`   | `pam_mail.so`
+   - `pam_nologin.so`  | `pam_permit.so`     | `pam_pwd.so`
+   - `pam_radius.so`   | `pam_rhosts_auth.so`| `pam_rootok.so`
+   - `pam_security.so` | `pam_shells.so`     | `pam_stress.so`
+   - `pam_tally.so`    | `pam_time.so`       | `pam_unix_acct.so`
+   - `pam_unix_auth.so`| `pam_unix_passwd.so`| `pam_unix_session.so`
+   - `pam_warn.so`     | `pam_wheel.so`      |

Some of the modules are only applicable for one type; others are applicable for all types (auth, account, password, session). All modules can take any control value (requisite, required, sufficient, optional). Table 15.1 lists these types and options.

Lines of modules are read line by line from the beginning of the file to the end unless a requisite or sufficient cause PAM to exit early.

> **Note:** Table 15.1 is not meant to be an exhaustive or even authoritative list of available PAM modules. If it were, it would be notable only for the modules not included or changed. Different distributions might even have different modules (ones written or modified by distribution-employed programmers, but not yet in general use). For more up-to-date information, see the documentation in `/usr/doc/libpam-<version>/`.