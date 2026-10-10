# > OPTIONS

+   - **debug**
+   Enable debugging output.

+   - **config_file=<*filena*>**
+   Sets the configuration file to use. Default value is */etc/pam_pkcs11/pam_pkcs11.conf*.

As it uses the sa configuration file as pam_pkcs11, all pam_pkcs11 options are also available. Note that so of them have no sense in a non-PAM environnt, so they will be ignored. So mapper options (mapfile, ignorecase) have no effect on certificate contents, so they will be ignored too.