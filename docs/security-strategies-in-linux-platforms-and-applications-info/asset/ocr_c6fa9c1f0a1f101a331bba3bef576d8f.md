# CHAPTER 4 | Privileges and Permissions

# 103

```
michael@ouderviceVM:~# apt-cache search libpam
libpam-ck-connect: Consolelet PAM module
libpam-crack: PAM module to enable cracklib
libpam-doc: Documentation PAM
libpam-gnome-keyring: PAM module to unlock the GNOME keyring upon login
libpam-kds: PAM module for MIT Kerberos
libpam-ldap: Pluggable Authentication Modules for LDAP
libpam-pam: Pluggable Authentication Modules for PAM
libpam-mount: PAM module that can mount volumes for a user session
libpam-opie: Use OTPs for PAM authentication
libpam-smart: PAM module for using smart cards
libpam-radius-auth: The PAM RADIUS authentication module
libpam-runtime: Runtime support for the PAM library
libpam-samamba: Pluggable authentication module for Samba
libpam-dev: Development files for PAM
opie-server: OTP programs for maintaining an OTP key file
upsd-superseded: pam module in libpam-modules
lapscripts: Add and remove user and groups (stored in a LDAP directory)
libpam-afs-session: PAM module to set a PAG and obtain AFS tokens
libpam-alreadylogged: PAM module to skip password authentication for logged users
libpam-apparmor: AppArmor library as a PAM module
libpam-blue: PAM module for local authentication with bluetooth devices
```

![](bbox=[0.735, 0.065, 0.885, 0.115])

PAM is configured in specific files in the /etc/pam.d/. These files, such as password and ssh, accurately depict the command or service that is regulated.

# The Structure of a PAM Configuration File

The structure of a PAM configuration file is based on its modules, available from the /lib/security/directory. If you don't find a desired module here, you may need to install another PAM-related package. Each line in a PAM configuration file is set up in the following format:

module_type control_flag module_file (arguments)

Older versions of PAM required the full path to the module. Current versions assume the module is in the /lib/security/ directory. If installed, more information on a module_file, such as the arguments used for a module, may be available from a man page. That leaves the module_type and control_flag options. First, there are four different module types:

+   * auth—Authenticates users by verifying passwords, group memberships, and even Kerberos tokens. Also known as authentication management.
* account—Checks the validity of the account based on expiration dates, time limits, or configuration files with restricted users. Also known as account management.
* password—Controls changes to user password. May also control the number of login attempts. Also known as password management.
* session—Makes the connection work; it may mount appropriate directories and information to system logs. Also known as session management.

There is an implicit default module type, include, which incorporates the configuration directives from another file.

![](bbox=[0.945, 0.535, 0.982, 0.635])