new modules and include them instead. New pluggable modules are being developed all the time, so it pays to watch the PAM Modules site: http://www.kernel.org/pub/linux/libs/pam/modules.html to see what is already out there.

Suppose there is an application that requires user authentication prior to performing some service for the user. In the old days, the application would have to request and read in a password and then validate that password or to use some other authentication scheme that was built into the application. Now, instead of using its own integrated authentication scheme, the PAM–aware application uses PAM to do the authentication portion.

To accomplish this, the application calls PAM, naming a configuration file, which usually shares the name of the application. If each application is free to have its own scheme as indicated by the existence of the /etc/pam.d directory, PAM looks there for a configuration file with the specified name. For example, the login program that is commonly used in Linux has a configuration file named /etc/pam.d/login. If PAM has been configured to apply the same authentication scheme to all applications, the scheme is determined by the /etc/pam.conf file.

The modules are pass–fail. By default, a failed authentication process proceeds past the failed module to prevent the user from knowing where the failure occurred and using this information to break the authentication. You can change this behavior by changing required to requisite in the configuration file; if any requisite module returns failure, PAM fails immediately without calling any other modules.

The /etc/pam.conf file contains a listing of services, each paired with a service module. When a service is requested, its associated module is invoked. Each entry has the following format:

```
```
*service_name* *module_type* *control_flag* *module_path* \[options\]
```
```

Each module referenced in the *module_path* for that service is then processed in the order in which it appears in the configuration file. The *control_flag* determines the persistence and importance of the modules and may be set to one of the following values: requisite, required, optional, or sufficient. If all requisite and required modules succeed, then a successful status is returned, and any errors in optional or sufficient modules are ignored. If any requisite or required modules fail, the error value from the first one that failed is returned. If no service modules are designated as requisite or required, at least one optional or sufficient module must succeed before a successful status is returned. If all fail, the error value from the first failed service module is returned. If two or more lines have the same *service_name* and *module_type* pair, that service is said to be *stacked*. This allows you to perform incremental checks with different parameters and set these checks to different levels of importance.

Recently a new syntax has been added to give PAM even more flexibility. Originally, PAM modules were strictly pass–fail. While this is still technically true since one failed module is a failure for the entire module, there is now room to allow for more in–depth control over individual return codes. The new syntax looks like this:

```
```
[value1=action1 value2=action2 ...]
```
```

Acceptable value tokens are listed below:

|   |   |
|:--|:--|
| success | cred_expired |
| open_err | cred_err |
| symbol_err | no_module_data |