
## Using Pluggable Authentication Modules (PAMs)

You may wonder how programs such as csh, chfn, ftp, imap, linuxconf, rlogin, rexe, rsh, su, login, and passwd suddenly understand the shadow password scheme and use the `/etc/shadow` password file for authentication. They can do so because Red Hat distributes these programs with shadow password capabilities. Actually, Red Hat ships these programs with a much grander scheme of authentication support called *Pluggable Authentication Modules (PAMs)*. These PAM-aware programs are capable of using not only the shadow password scheme but also virtually any other authentication scheme that you care to implement to enhance your system security.

Traditionally, authentication schemes are built into programs that grant privileges to users. Programs such as login or passwd used to be built with the necessary code to handle authentication. Over time, this approach proved to be virtually nonscalable, because incorporating a new authentication scheme required that privilege-granting programs had to be recoded and recompiled. To relieve the privilege-granting software developer from having to write secure authentication code, PAM was developed. Figure 15-1 shows how PAM works with privilege-granting applications.

When a privilege-granting application such as `/bin/login` is made into a PAM-aware application, it typically works in the manner shown in Figure 15-1 and described in the numbered steps that follow.

1. First, a user invokes such an application to access the service it offers.
2. The PAM-aware application calls the underlying PAM library to perform the authentication.
3. The PAM library looks up an application-specific configuration file in the `/etc/pam.d/` directory. This file tells PAM what type of authentication is required for this application.
4. The PAM library loads the required authentication module(s).

### Figure 15-1 How PAM-aware applications work

![](img/f9ec99365f159bfe663f8ac29732663c_452_0.png)

5. These modules can then make PAM communicate with the conversation functions available in the application.
6. The conversation functions can be used to request information from the user. For example, the user can be asked to enter a password or look into a retinal scanner.
7. The user responds to the request by providing requested information.
8. The PAM authentication modules supply the application with an authentication status message via the PAM library.
9. If the authentication process is successful, the application grants the requested privileges to the user or informs the user that the process failed.

Think of PAM as a facility that takes the burden of authentication away from the applications and allows you to stack multiple authentication schemes for a single application. For example, the PAM configuration file for the rlogin application is shown in Listing 15-1.

### Listing 15-1 The /etc/pam.d/login file

```
auth             required       /lib/security/pam_security.so
auth             sufficient     /lib/security/pam_rhosts_auth.so
auth             required       /lib/security/pam_pwd.so shadow nullok
auth             required       /lib/security/pam_nologin.so
account          required       /lib/security/pam_pwdb.so
password         required       /lib/security/pam_cracklib.so
password         required       /lib/security/pam_pwd.so shadow nullok
 \ use_autotok
session          required       /lib/security/pam_pwdb.so
```

In this file, multiple authentication modules from /lib/security are used to authenticate the user.

## Working with a PAM configuration file

Listing 15-1 shows what an application-specific PAM configuration file looks like. Lines starting with a leading # and blank lines are ignored. A configuration line has the following fields:

```
module-type control-flag module-path module-args
```

Currently, four module types exist, which are described in Table 15-2.

**Table 15-2 PAM Module Types**

| Module Type | Description |
| :--- | :--- |
| auth | Does the actual authentication. Typically, an auth module requires a user to enter a password or provide some other proof of identity. |
| account | Handles all the accounting aspects of an authentication request. Typically, an account module checks whether the user access meets all the access guidelines. For example, it can check whether the user is accessing the service from a secure host and during a specified time. |
| password | Handles things that need to be done before and after the user is given access to the requested service. |
| session | Used to handle session management tasks, such as refreshing session tokens. |

The control flag is used to define how the PAM library will handle a module's response. Four control flags, described in Table 15-3, are currently allowed.

**Table 15-3 PAM Control Flags**

| Control Flag | Description |
| :--- | :--- |
| required | Specifies that the success of the module specified in the same line is a requirement. Even if module returns a response indicating failure, the authentication will definitely fail, but PAM will continue with other modules (if any). This is done to ensure that the user cannot detect which part of the authentication process failed, because knowing that information might aid a potential attacker. |
| requisite | When this control flag is used, the authentication process aborts as soon as a failure response is received by the PAM library. |
| sufficient | When this control flag is used, the authentication process is considered complete if a success response is received. In other words, proceeding with other modules in the configuration file is unnecessary. |
| optional | This control flag is hardly used; it does not put any emphasis on the success or failure response of the module. |

The module path is the path of a pluggable authentication module. Red Hat Linux stores all the PAMs in the /lib/security directory. You can supply each module with optional arguments, as well.

Looking back at Listing 15-1, notice that the PAM library calls the pam_security.so module, which must return a response indicating success in order for the authentication to be successful. If the module's response indicates failure, PAM will still continue processing the other modules so that the user (who could be a potential attacker) is not aware of where the failure occurred. If the next module (pam_rhosts_auth.so) returns a success response, the authentication process is complete, because the control flag is set to sufficient. However, if the previous module (pam_security.so) does not fail but this one fails, the authentication process will continue and the failure will not affect the final result. In the same fashion, the PAM library will process the rest of the modules.

The order of execution exactly follows the way the modules appear in the configuration. However, each type of module (auth, account, password, and session) will be processed in a stack. In other words, for the example in Listing 15-1, all the auth modules will be stacked and processed in order of appearance in the configuration file. The rest of the modules will be processed in a similar fashion.

## Using PAM to fine-tune the authentication process

Now that you know so much about how PAM works, consider an example of how you can use PAM to fine-tune authentication processes for certain services. The very first step you should take is to read the documentation for all the available PAMs. All the available PAMs are stored in the `/lib/security` directory, and you can find documentation on each module in the `/usr/doc/pam-x.xx` directory, where `x.xx` is your PAM version. Read the documentation for each module and determine which you want to use in building a more restrictive authentication scheme for your system. In this section, I will show you how you can restrict login access to your server by time.

To restrict access to services by time, you need an accounting module called pam_time (`/lib/security/pam_time.so`). This module can be configured to deny access to individual users based on their name, the time of day, the day of the week, the service they are applying for, and the terminal from which they are making their request. Its actions are determined with the `/etc/security/time.conf` configuration file.

Because you want to control login access, you need to modify the `/etc/pam.d/login` PAM configuration file by adding the following line:

```
account required /lib/security/pam_time.so
```

Next, you need to devise an access policy for login service. In other words, you need to determine when you want users to be able to log in. This example assumes that you want to allow users to be able to log in after 6 a.m. and no later than 8 p.m. Now, you need to configure the `/etc/security/time.conf` file. The configuration lines in this file have the following syntax:

```
services:tts:users:times
```

You can use some special characters in each of the fields. Table 15-4 shows the meaning of the special characters you can use.
