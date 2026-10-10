
## Chapter 16
### Looking at Access and Authentication Methods

![](img/c0a399aca0d18f8822d714ad0a173123_534_0.png)

- **Objective 2.1:** Summarize the purpose and use of security best practices in a Linux environment.
- **Objective 2.2:** Given a scenario, implement identity management.
- **Objective 2.4:** Given a scenario, configure and execute remote connectivity for system management.

![](img/c0a399aca0d18f8822d714ad0a173123_535_0.png)

Part of properly securing a system and its data involves providing appropriate access and authentication methods. There are many tools available to provide these services.

However, it is crucial to understand how they work and how to configure them appropriately.

We’ll take a look at the various authentication and access methods, where their configuration files are stored, and how to properly configure them. We’ll cover some important encryption and authentication topics as well.

### Getting to Know PAM

Pluggable authentication modules (PAMs) provide centralized authentication services for Linux and applications. Sun Microsystems started the Linux-PAM project in 1997 to explore using pluggable authentication in a Linux environment. Today, PAM is typically used on all Linux distributions.

PAM provides authentication libraries that compile into the application, becoming an interface the application requiring authentication and an authentication method. It supports lots of different underlying authentication libraries (called modules), including:

- **Password:** PAM supports using both the `/etc/passwd` and `/etc/shadow` password files to authenticate using a text password.
- **Certificate:** PAM can use public key infrastructure (PKI) certificate stores to authenticate users.
- **Lightweight Directory Access Protocol (LDAP):** PAM can connect to a centralized LDAP server in an organization to support network logins.
- **Kerberos:** PAM supports the Kerberos authentication system, which issues a token to clients when they log into the system. These tokens can then be used for authentication on multiple network resources. This process is often referred to as single sign-on (SSO), where you need to log in just once to access multiple resources on the network.
- **Multifactor authentication (MFA):** PAM supports several types of MFA environments, such as biometrics, tokens, PKI, and one-time passwords emailed to users.

The beauty of PAM is that programs don’t need to change anything to utilize different authentication methods—PAM controls that all with configuration files. Programs that use PAM services are compiled with the PAM library, `libpam.so`, and have an associated PAM configuration file. Applications that use PAM are called “PAM-aware.” You can quickly determine if a program is PAM-aware by using the `ldd` command. A snipped example is shown in Listing 16.1.

**Listing 16.1: Using ldd to determine if application is PAM-aware**

```
# ldd /bin/login | grep libpam.so
libpam.so.0 => /lib64/libpam.so.0 (0x00007fbf2ce17000)
#
```

In Listing 16.1, the `ldd` utility is employed to display all the program's shared library dependencies. The display output is piped into `grep` to search for only the PAM `libpam.so` library. In this case, the application is compiled with the PAM library. Besides being compiled with the PAM `libpam.so` library, the application needs to have a configuration file to use PAM.

### Exploring PAM Configuration Files

PAM configuration files are located in the `/etc/pam.d/` directory. Listing 16.2 shows this directory's files on a Rocky Linux distribution.

**Listing 16.2: Viewing the /etc/pam.d/ directory's contents**

```
$ ls /etc/pam.d/
atd		gdm-fingerprint	pluto		su
chfn		gdm-launch-environment polkit-1		sudo
chsh		gdm-password	postlogin		sudo-
cockpit		gdm-pin		remote		su-
config-util	gdm-smartcard	runuser		system-auth
crond		login		runuser-l		systemd-user
cups		other		smartcard-auth	vlock
fingerprint-auth	passwd		sshd		vmtoolsd
gdm-autologin	password-auth	sssd-shadowutils	xserver
$
```

Notice in Listing 16.2 that there is a `login` configuration file. This file is displayed snipped in Listing 16.3.

**Listing 16.3: Viewing the /etc/pam.d/login file's contents**

```
$ cat /etc/pam.d/login
#%PAM-1.0
[..]
auth		include		postlogin
account		required		pam_nologin.so
account		include		system-auth
password		include		system-auth
[..]
session		optional		pam_keyinit.so force revoke
[..]
$
```

The records in a PAM configuration file have a specific syntax:

`type` `control-flag` `pam-module` `[module-options]`

The type (*TYPE*), sometimes called a *context* or *module interface*, designates a particular PAM service type. The four PAM service types are shown in Table 16.1.

**TABLE 16.1** *TYPE in* `/etc/pam.d/` *configuration file records*

| Interface | Service description |
| :--- | :--- |
| account | Implements account validation services, such as enforcing time-of-day restrictions as well as determining if the account has expired |
| auth | Provides account authentication management services, such as asking for a password and verifying that the password is correct |
| password | Manages account passwords, such as enforcing minimum password lengths and limiting incorrect password entry attempts |
| session | Provides authenticated account session management for session start and session end—such as logging when the session began and ended—as well as mounting the account’s home directory, if needed |

The *PAM-MODULE* portion of the `/etc/pam.d/` configuration file record is simply the filename of the module that will be doing the work. For example, *pam_nologin.so* is shown in the `/etc/pam.d/login` configuration file in Listing 16.3. Additional module options can be included after the module’s filename.

A designated *PAM-MODULE* is called in the order in which it is listed within the PAM configuration file. This is called the *module stack*. Each *PAM-MODULE* returns a status code, which is handled via the record’s *CONTROL-FLAG* setting. Together these status codes and settings create a final status, which is sent to the application. Table 16.2 lists the various control flags and their responses or actions.

**TABLE 16.2** *The* *CONTROL-FLAG* *settings for* `/etc/pam.d/` *configuration file records*

| Control flag | Description |
| :--- | :--- |
| include | Adds status codes and response ratings from the designated PAM configuration files into the final status. |
| optional | Conditionally adds the module’s status code to the final status. If this is the only record for the PAM service type, it is included. If not, the status code is ignored. |
| requisite | If the module returns a fail status code, a final fail status is immediately returned to the application without running the rest of the modules within the configuration file. |
| required | If the module returns a fail status code, a final fail status will be returned to the application, but only after the rest of the modules within the configuration file run. |
| substack | Forces the included configuration files of a particular type to act together returning a single status code to the main module stack. |
| sufficient | If the module returns a success status code and no preceding stack modules have returned a fail status code, a final success status is immediately returned to the application without running the rest of the modules in the configuration file. If the module returns a fail status code, it is ignored. |

The `/etc/pam.d/` configuration files' module stack process of providing a final status is a little confusing. A simplification to help you understand the progression is depicted in Figure 16.1.

**FIGURE 16.1** The PAM module stack process

![](img/c0a399aca0d18f8822d714ad0a173123_538_0.png)

Using Figure 16.1 as a guide, imagine that the application subject (user) needs authentication to access the system. The appropriate `/etc/pam.d/` configuration file is employed. Going through the authentication module stack, the user passes through the various security checkpoints. At each checkpoint, a guard (PAM module) checks a different requirement, determines whether or not the user has the required authentication, and issues a fail or success card. The final guard reviews the status cards along with their control flags listed on a clipboard. This guard determines whether or not the subject may proceed through the “System Access” doorway. Of course, keep in mind that if any of the checkpoints are listed as requisite, and the user fails that checkpoint, they would be immediately tossed out.
