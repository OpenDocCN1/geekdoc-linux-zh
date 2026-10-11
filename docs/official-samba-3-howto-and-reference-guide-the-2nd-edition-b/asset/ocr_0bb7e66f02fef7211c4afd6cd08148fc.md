We explain the meaning of each of these tokens. The second (and more recently adopted) way of configuring Linux-PAM is via the contents of the /etc/pam.d/ directory. Once we have explained the meaning of the tokens, we describe this method.

**service-name** The name of the service associated with this entry. Frequently, the service-name is the conventional name of the given application — for example, `ftpd`, `logind` and `su`, and so on.

There is a special service-name reserved for defining a default authentication mechanism. It has the name OTHER and may be specified in either lower- or uppercase characters. Note, when there is a module specified for a named service, the OTHER entries are ignored.

**module-type** One of (currently) four types of module. The four types are as follows:

+   - **auth**: This module type provides two aspects of authenticating the user. It establishes that the user is who he or she claims to be by instructing the application to prompt the user for a password or other means of identification. Second, the module can grant group membership (independently of the /etc/groups file) or other privileges through its credential-granting properties.

+   - **account**: This module performs non-authentication-based account management. It is typically used to restrict/permit access to a service based on the time of day, currently available system resources (maximum number of users), or perhaps the location of the user login. For example, the "root" login may be permitted only on the console.

+   - **session**: Primarily, this module is associated with doing things that need to be done for the user before and after he or she can be given service. Such things include logging information concerning the opening and closing of some data exchange with a user, mounting directories, and so on.

+   - **password**: This last module type is required for updating the authentication token associated with the user. Typically, there is one module for each “challenge/response” authentication (auth) module type.

**control-flag** The control-flag is used to indicate how the PAM library will react to the success or failure of the module it is associated with. Since modules can be stacked (modules of the same type execute in series, one after another), the control-flags determine the relative importance of each module. The application is not made aware of the individual success or failure of modules listed in /etc/pam.conf file. Instead, it receives a summary success or fail response from the Linux-PAM library. The order of execution of these modules is that of the entries in the /etc/pam.conf file; earlier entries are executed before later ones. As of Linux-PAM v0.60, this control-flag can be defined with one of two syntaxes.