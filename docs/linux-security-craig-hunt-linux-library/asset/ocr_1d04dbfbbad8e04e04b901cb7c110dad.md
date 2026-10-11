+   * Systems administrators must manage heterogenous authentication mechanisms.

Originally developed by Sun Microsystems, the Pluggable Authentication Modules (PAM) framework allows administrators to control authentication parameters for network applications. Developers simply adhere to the PAM standard and call a set of dynamic libraries that come with PAM. PAM support is now included in all major Linux distributions, and a growing number of network applications are now using PAM for authentication.

There are two parts to the PAM system:

+   * A set of dynamically linked shared libraries (modules) that are typically installed in `/lib/security` or `/usr/lib/security`

+   * A set of configuration files that are typically installed in `/etc/pam.d/`

The developer of a networked application (for example, `login`) simply specifies that authentication is needed in the code before the user is granted a shell. You, as the system administrator, have complete control, using the `/etc/pam.d/login` configuration file, to specify what type of authentication you want your users to undergo before `login` gives them access to their shell.

The tasks that PAM takes care of fall into four categories or management groups:

+   * Authentication management, where PAM establishes whether the user is who they claim to be. This can be achieved using a simple method like standard username/ passwords, using a more complex method such as challenge-response authentication, or using a time-based hardware token card.

+   * Account management, where PAM provides verification services based on the account information. This management group concerns itself with questions like

+   * Has the user password expired?
+   * Does this user belong to the right group to be allowed access to a particular service?

+   * Password management, where PAM takes care of any necessary updates to the authentication token associated with the user. Once the user is authenticated, the password management group prompts a user for a new password if the previous has expired.

+   * Session management, where PAM does a number of things in preparation for granting the user access to the resources or right before the service is to be withdrawn. Session management tasks include logging events, mounting home directories, etc.

![](bbox=[0.91, 0.6, 0.99, 0.81])