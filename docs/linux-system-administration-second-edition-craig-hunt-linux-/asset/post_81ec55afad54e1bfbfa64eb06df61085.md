
their password hashes to the /etc/passwd file. Keep in mind that the password aging information stored in /etc/shadow will be lost in this transaction.

If you enable shadow passwords using authconfig, it will transfer the hashes from the /etc/passwd file to the /etc/shadow file, replacing each hash in /etc/passwd with an X. This can be accomplished outside of authconfig by the pwconv command, which converts to shadow passwords by moving the hashes from /etc/passwd file to /etc/shadow. Use pwunconv to go the other direction.

For any additional information, read the Shadow-Password-HOWTO available at the Linux Documentation Project: http://www.tldp.org/HOWTO/Shadow-Password-HOWTO.html.

## Pluggable Authentication Modules (PAM)

At first, most privileges were granted based on password authentication or membership in a specific group. That was not a bad beginning. It soon became obvious, however, that it was insufficient to assume that a user's identity is known simply because the login password is correct and rely on that authentication as the sole means of determining what access should be granted. New programs began including their own authentication methods instead of assuming that the login authentication was sufficient. Each authentication method required the login, FTP, and other programs to be rewritten to support it.

Now authentication is more flexible and is handled under Linux by Pluggable Authentication Modules (PAM). The different major distributions began including PAM in the following versions: Red Hat Linux 5.0, Debian Linux 2.1, Caldera Linux 1.3, and SuSE Linux 6.2.

PAM is a flexible set of library modules that allow a system administrator to configure each individual application with its own authentication mechanism—a defined subset of the available library modules. Although some operating systems look for their PAM loadable object files in /usr/lib/security, Red Hat chose to follow the Linux Filesystem Standard by locating them in /lib/security. A listing of this directory includes a number of files with names like pam_access.so, pam_console.so, pam_cracklib.so, and so on. These files are the shared libraries that support the various capabilities of PAM.

Any program that uses PAM modules instead of some internal security method is called a PAM client. PAM uses four basic modules to authenticate users, manage user accounts, manage passwords, and manage actual login sessions. The authentication module is responsible for both verifying the user's credentials and giving the okay to proceed. The account management module provides the capability to determine if the current user's account is valid. This module checks for password or account expiration and verifies that the login meets any restrictions like access hours or maximum number of users. The password module provides functionality to change a user's authentication token or password. A session management module provides functionality to set up and terminate login sessions and performs any setup tasks such as mounting required directories. These modules are referenced in the configuration file, which we'll look at below.

In order to work with PAM, applications are developed to be independent of any particular authentication scheme. This means that the program is no longer concerned with which authentication scheme it will use. Instead, it will have "authentication modules" attached to it at runtime in order to work. The Linux administrator can change the authentication scheme for a PAM-aware application at any time, without rewriting the application code, by editing a PAM configuration file, which may be application-specific or used system-wide. The modules referenced within the configuration file implement the authentication scheme; so to change schemes, you edit the file to include different modules. If no existing modules meet your security needs, you may write new modules and include them instead. New pluggable modules are being developed all the time, so it pays to watch the PAM Modules site: http://www.kernel.org/pub/linux/libs/pam/modules.html to see what is already out there.

Suppose there is an application that requires user authentication prior to performing some service for the user. In the old days, the application would have to request and read in a password and then validate that password or to use some other authentication scheme that was built into the application. Now, instead of using its own integrated authentication scheme, the PAM-aware application uses PAM to do the authentication portion.

To accomplish this, the application calls PAM, naming a configuration file, which usually shares the name of the application. If each application is free to have its own scheme as indicated by the existence of the /etc/pam.d directory, PAM looks there for a configuration file with the specified name. For example, the login program that is commonly used in Linux has a configuration file named /etc/pam.d/login. If PAM has been configured to apply the same authentication scheme to all applications, the scheme is determined by the /etc/pam.conf file.

The modules are pass-fail. By default, a failed authentication process proceeds past the failed module to prevent the user from knowing where the failure occurred and using this information to break the authentication. You can change this behavior by changing required to requisite in the configuration file; if any requisite module returns failure, PAM fails immediately without calling any other modules.

The /etc/pam.conf file contains a listing of services, each paired with a service module. When a service is requested, its associated module is invoked. Each entry has the following format:

```
*service_name* *module_type* *control_flag* *module_path* [options]
```

Each module referenced in the *module_path* for that service is then processed in the order in which it appears in the configuration file. The *control_flag* determines the persistence and importance of the modules and may be set to one of the following values: requisite, required, optional, or sufficient. If all requisite and required modules succeed, then a successful status is returned, and any errors in optional or sufficient modules are ignored. If any requisite or required modules fail, the error value from the first one that failed is returned. If no service modules are designated as requisite or required, at least one optional or sufficient module must succeed before a successful status is returned. If all fail, the error value from the first failed service module is returned. If two or more lines have the same *service_name* and *module_type* pair, that service is said to be *stacked*. This allows you to perform incremental checks with different parameters and set these checks to different levels of importance.

Recently a new syntax has been added to give PAM even more flexibility. Originally, PAM modules were strictly pass-fail. While this is still technically true since one failed module is a failure for the entire module, there is now room to allow for more in-depth control over individual return codes. The new syntax looks like this:

```
[value1=action1 value2=action2 ...]
```

Acceptable value tokens are listed below:

| Token 1 | Token 2 |
| :--- | :--- |
| success | cred_expired |
| open_err | cred_err |
| symbol_err | no_module_data |
| service_err | conv_err |
| system_err | authtok_err |
| buf_err | authtok_recover_err |
| perm_denied | authtok_lock_busy |
| auth_err | authtok_disable_aging |
| cred_insufficient | try_again |
| authinfo_unavail | ignore |
| user_unknown | abort |
| maxtries | authtok_expired |
| new_authtok_reqd | module_unknown |
| acct_expired | bad_item |
| session_err | default |
| cred_unavail | |

There are six action tokens: ignore, ok, done, bad, die, reset, or some positive integer. The integer value represents how many occurrences of value to skip before taking an action. The action ignore indicates that the value is not to be passed back to the application; for example, a failure that might normally cause a user to be denied access might be masked by the PAM module, thereby having no effect. The action ok indicates that the return code is important enough to affect the entire PAM stack. As before, if the PAM stack's return code is PAM_SUCCESS before this value-action pair, this return code will affect the stack; however, if the PAM stack already showed failure, a successful return code will not override the previous stack state, since one failure is enough for the stack to fail completely. The action done is the same as ok except that PAM does not continue further through the stack but terminates and returns to the application. The action bad indicates failure for the entire PAM stack but PAM continues through the rest of the stack. The action die is similar to bad except that the processing of the PAM stack is terminated and control is returned to the application. The reset action clears the memory of the PAM stack's state and continues to the next stacked module.

Originally, if any entry in /etc/pam.conf was incorrect, or if a module could not be opened, all PAM services would fail, and users were not permitted access to the system. Using the newer value-action pairs, it is possible to allow for different behavior. For instance, you might allow for six bad item return codes before actually failing the module. Likewise if the system is missing the appropriate file in /etc/pam.d, or if the /etc/pam.conf file has been deleted, no one will be able to log into the system since login is the first of the applications that rely on PAM. To fix this, the system administrator must use single-user mode to correct the errant file or to reinstall PAM completely.

If your system is set up to use different authentication schemes for each application, each will have its own configuration file located in /etc/pam.d. The general syntax of an /etc/pam.d configuration file is as follows:

```
module_type control_flag module_path [arguments]
```

On Red Hat 7.3, the /etc/pam.d/login configuration file looks like Listing 15.5. Let's walk through it to see how it works.

### Listing 15.5: The /etc/pam.d/login Configuration File for Red Hat

```
#%PAM-1.0
auth        required    /lib/security/pam_sepermit.so
auth        required    /lib/security/pam_stack.so service=system-auth
auth        required    /lib/security/pam_nologin.so
account     required    /lib/security/pam_stack.so service=system-auth
```
