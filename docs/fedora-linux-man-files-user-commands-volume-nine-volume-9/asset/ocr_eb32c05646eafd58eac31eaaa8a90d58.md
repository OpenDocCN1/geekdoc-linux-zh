# DESCRIPTION

**pkcs11_inspect** uses the pam_pkcs11 library infrastructure to get the content of a certificate and display it.

**pkcs11_inspect** uses the sa configuration file and argunts than (8) PAM module. It loads defined mapper modules, and use them to look into the certificate for required entries (ie: ms_mapper looks for ms UPN entries, and so on).

When a mapper module finds a proper entry in the certificate, it converts to UTF-8 and print it to stdout.