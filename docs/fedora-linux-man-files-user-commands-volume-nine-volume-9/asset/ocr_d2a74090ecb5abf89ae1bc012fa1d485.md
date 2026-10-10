# DESCRIPTION

**setup-nsssysinit**

is a shell script to query the status of the nss-sysinit module and when run with root privilege it can enable or disable it.

Turns on or off the nss-sysinit module db by editing the global PKCS #11 configuration file. Displays the status. This script can be invoked by the user as super user. It is invoked at nss-sysinit post install ti with argument on.