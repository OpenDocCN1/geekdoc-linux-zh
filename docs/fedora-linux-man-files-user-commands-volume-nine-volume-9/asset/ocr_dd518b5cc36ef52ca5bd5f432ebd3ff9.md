# OPTIONS

+   * **debug**
+       Enable debugging output. Default is no debug.
+     
+     * **config_file**=<configuration file>
+       Sets the configuration file to use. Default value is /etc/pam_pkcs11/pam_pkcs11.conf.

As it uses the sa configuration file than pam_pkcs11, all pam_pkcs11 options are also available. Note that so of them has no sense in a non-PAM enviromnt, so they will be ignored.