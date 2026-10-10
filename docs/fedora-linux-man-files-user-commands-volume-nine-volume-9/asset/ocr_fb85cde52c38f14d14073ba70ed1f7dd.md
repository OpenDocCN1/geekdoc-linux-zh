# ## DESCRIPTION

**pklogin_finder** uses the pam_pkcs11 library infrastructure to interactively map a PKCS#11 provided certificate to a user.

**pklogin_finder** uses the the sa configuration file and argunts than (8) PAM module. Load defined mapper modules, and try to find a map between found certificates and a user login.