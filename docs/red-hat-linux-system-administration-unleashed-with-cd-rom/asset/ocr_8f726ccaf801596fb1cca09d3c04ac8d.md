isn't a word straight out of the dictionary. It can also make sure the password is of a certain length and contains a certain mix of different kinds of characters (letters, numbers, punctuation, and so on). In Red Hat, PAM comes pre-installed and uses /etc/pam.d to store most of its configuration files. There is one file for each service that requires authentication, with the filename being the same as the name of the service. Inside each configuration file is a list of things PAM should do when authentication is required or when changing authentication parameters. The lines form a stack of tasks for PAM to perform in order to do the required authentication for the application. Each step in a stack performs a different function. Some will affect the general pass/fail outcome of the entire stack, and some will merely log information about the state as the user proceeds through the stack. The file consists of several lines of the following format:

```
service-name module-type control-flag module-path arguments
```

The service-name is frequently the conventional name of the application such as ftpd, rlogind, and so on. There is also a special service-name reserved for defining a default authentication mechanism, it is called other.

At present there are only four possible module-types. They are

+   - auth—Verify that users are who they say they are (request a password).
+   - account—Restrict/permit access to services.
+   - session—Preconfiguration before granting the service to someone, or post-configuration after granting the service to someone.
+   - password—Update the authentication token for this user.

Like the module-type parameter, there are four possible control-flag parameters. These indicate the level of concern if a particular module succeeds or fails. The control-flag keywords are

+   - required—Necessary for successful authentication. Failure will not be apparent to the user until all other modules have finished.
+   - requisite—Similar to required, but module exits immediately on failure.
+   - sufficient—Meets the criteria for success for this module.
+   - optional—Used only in the case of an indeterminate response from other modules in the stack.