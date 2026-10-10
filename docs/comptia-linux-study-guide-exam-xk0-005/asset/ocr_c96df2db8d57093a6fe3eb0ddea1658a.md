The records in a PAM configuration file have a specific syntax:

*type* *control-flag* *pam-module* [*module-options*]

The type (*TYPE*), sometimes called a *context* or *module interface*, designates a particular PAM service type. The four PAM service types are shown in Table 16.1.

# **TABLE 16.1** *TYPE in* `/etc/pam.d/` *configuration file records*

| Interface | Service description |
| :--- | :--- |
| account | Implements account validation services, such as enforcing time-of-day restrictions as well as determining if the account has expired |
| auth | Provides account authentication management services, such as asking for a password and verifying that the password is correct |
| password | Manages account passwords, such as enforcing minimum password lengths and limiting incorrect password entry attempts |
| session | Provides authenticated account session management for session start and session end—such as logging when the session began and ended—as well as mounting the account’s home directory, if needed |

The *PAM-MODULE* portion of the `/etc/pam.d/` configuration file record is simply the filename of the module that will be doing the work. For example, *pam_nologin.so* is shown in the `/etc/pam.d/login` configuration file in Listing 16.3. Additional module options can be included after the module’s filename.

A designated *PAM-MODULE* is called in the order in which it is listed within the PAM configuration file. This is called the *module stack*. Each *PAM-MODULE* returns a status code, which is handled via the record’s *CONTROL-FLAG* setting. Together these status codes and settings create a final status, which is sent to the application. Table 16.2 lists the various control flags and their responses or actions.

# **TABLE 16.2** *The* *CONTROL-FLAG* *settings for* `/etc/pam.d/` *configuration file records*

| Control flag | Description |
| :--- | :--- |
| include | Adds status codes and response ratings from the designated PAM configuration files into the final status. |
| optional | Conditionally adds the module’s status code to the final status. If this is the only record for the PAM service type, it is included. If not, the status code is ignored. |
| requisite | If the module returns a fail status code, a final fail status is immediately returned to the application without running the rest of the modules within the configuration file. |