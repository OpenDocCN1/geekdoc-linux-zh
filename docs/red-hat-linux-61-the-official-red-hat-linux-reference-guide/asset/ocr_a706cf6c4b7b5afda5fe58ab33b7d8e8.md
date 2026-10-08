# Chapter 17. Kerberos

1. Be sure you have clock synchronization and DNS on your server before configuring Kerberos 5. Particular attention to time synchronization between the Kerberos server and its various clients. The server and client clocks differ by more than five minutes (this default is configurable in Kerberos 5), Kerberos clients will not be able to authenticate to the server. This clock synchronization is necessary to prevent an attacker from using an old Kerberos ticket to masquerade as a user.

You should set up a Network Time Protocol (NTP) mapping client/server network if you are not using Kerberos. Hat Linux includes the ntp for easy installation. /usr/share/doc/ntp-<version-number>/index.htm for details on setting up Network Time protocol and for additional information on NTP.

2. Install the kb5-libs, kb5-server, and kb5-workstation packages on the dedicated machine which will run the KDC. This machine needs to be very secure — if possible, you should not run any services other than the KDC.

If you would like to use a graphical user interface to administer Kerberos, you should install the gnome-kerberos package. It contains kb5, a GUI tool for managing tasks.

3. Edit the /etc/kerberos/krb5.conf and /var/kerberos/krb5kdc/krb5.conf configuration files to reflect your realm name and domain-to-realm mappings. A simple realm can be constructed by replacing instances of EXAMPLE, example.com with your domain name — by changing to keep uppercase and lowercase names in the correct format — and changing the KDC from Kerberos, example.com to the name of your Kerberos server. By convention, all realm names are uppercase and all DNS hostnames and domain names are lowercase. For full details on the files, see respective pages.

4. Create the database using the kb5_util utility from a prompt:
/usr/kerberos/sbin/kb5_util create -s

The create command creates the database that will store keys for your Kerberos server. The -s switch forces creation of a file in which the master server key is stored. The Kerberos server (krb5kdc) will prompt the user for server password (which can be used to regenerate the key) every time it accesses. Most organizations have administrative access to the Kerberos database and their level of access.

5. Edit the /var/kerberos/krb5kdc/kadm5.acl file. This file is used by kadmin to determine which principals have administrative access to the Kerberos database and. Most organizations will be set by a single line:
*admin@EXAMPLE.COM

Most users are represented in the database by a single principal (with a NULL, or empty, such as joe@EXAMPLE.COM). With this configuration, users with a second principal with an instance of admin (for example, joe/admin@EXAMPLE.COM) will be able to wield power over the Kerberos database.

Once kadmin is started on any of the clients or servers in the realm, you will be able to access its services by naming kadmin. However, only users listed in the kadm5.acl file will be able to modify the database in any way, except for changing their own passwords.

![](bbox=[0.115, 0.798, 0.155, 0.825])

> Note
Theadmin utility communicates with the kadmin server over the network, and they use Kerberos to handle authentication. Of course, you need to create the first principal before you can connect to the server to administer it. The first principal with kadmin.local command, which is specifically designed to be used on the same host as the KDC and does not use Kerberos for authentication.

By typing kadmin.local command at the KDC terminal to create the first principal: