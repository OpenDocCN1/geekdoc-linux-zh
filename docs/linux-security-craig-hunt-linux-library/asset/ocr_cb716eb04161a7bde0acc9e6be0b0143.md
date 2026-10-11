To force the root user to use a secure terminal, add the following directives to /etc/pam.d/login as the first line in the file:
auth required pam_secruity.so

# # The pam_unix Module

The pam_unix module is the standard Unix authentication module. It uses standard calls from the system’s libraries to retrieve and set account information as well as to perform authentication. Usually this is information is obtained from the /etc/passwd file, and from the /etc/shadow file as well if shadow is enabled.

The arguments available on the pam_unix module vary according to the management group in question.

Account The arguments for the account management group are as follows:

+   * debug: This option makes the module write diagnostic information to syslog.
+   * audit: This option forces additional (more pedantic) information to be written to syslog.

Authentication The arguments for the authentication management group are as follows:

+   * debug: This argument makes the pam_unix module write diagnostic information to syslog.
+   * audit: This argument forces additional (more pedantic) information to be written to syslog.
+   * use_first_pass: This argument forces the pam_unix module attempt to use the previous stacked authentication module’s password and effectively never prompts the user for one. Note that if no password is available or the password is not appropriate, the user is denied access altogether.
+   * try_first_pass: This argument forces the pam_unix module to attempt the previous stacked authentication module’s password in case that satisfies this module as well.
+   * nullok: By default, the pam_unix module does not permit the user access to a service if their password is blank. The nullok argument overrides this default.
+   * nodeelay: By default, the pam_unix module requests a delay-on-failure of the order of one second. The nodeley argument discourages the authentication component from requesting a delay should the authentication as a whole fail.

Password The arguments for the password management group are as follows:

+   * debug: This argument makes the pam_unix module write diagnostic information to syslog.