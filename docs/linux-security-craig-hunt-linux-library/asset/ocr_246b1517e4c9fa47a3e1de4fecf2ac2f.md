kadmin/change pw. These two principals are automatically created by Kerberos when the database is first generated. You use the kadmin. local command, as before, to create the keytabs, as shown in Listing 13.6.

# **Listing 13.6**  Creating the keytabs with kadmin.local

```
[ramon]$ sudo /usr/kerberos/sbin/kadmin.local
Authenticating as principal root/admin@HONTANON.COM with password.
kadmin.local: kttadd -k /var/kerberos/krb5kdc/kadm5.keytab kadmin/admin
Entry for principal kadmin/admin with kvno 4, encryption type DES-cbc cbc mode with CRC-32 added to keytab WRFILE:/var/kerberos/krb5kdc/kadm5.keytab.
Entry for principal kadmin/admin with kvno 4, encryption type Triple DES cbc mode raw added to keytab WRFILE:/var/kerberos/krb5kdc/kadm5.keytab.
Entry for principal kadmin/changepw with kvno 4, encryption type DES cbc mode with CRC-32 added to keytab WRFILE:/var/kerberos/krb5kdc/kadm5.keytab.
Entry for principal kadmin/changepw with kvno 4, encryption type Triple DES cbc mode raw added to keytab WRFILE:/var/kerberos/krb5kdc/kadm5.keytab.
```

The kttadd command is invoked with the -k switch, followed by the location of the keytab file. This file should match the value of the admin_keytab variable in the kdc.conf file (/var/kerberos/krb5kdc/kadm5.keytab in the example earlier in this section).

You are now ready to start both the main KDC daemon and the administration daemon with the following commands:

```
[ramon]$ sudo /usr/kerberos/sbin/krb5kdc
[ramon]$ sudo /usr/kerberos/sbin/kadmin
```

Once the commands have been entered, the processes will fork and move into the background, freeing up your terminal for other work. If you want these processes to start at system boot time, you can add symbolic links to the scripts

```
/etc/rc.d/init.d/krb5kdc
/etc/rc.d/init.d/kadmin
```

to the /etc/rc.d/rc5.d directory.

> **NOTE**  If at all possible, dedicate a system to perform the KDC functions exclusively. Running other services (FTP, WWW, and SMTP) on the KDC increases the risk that the Kerberos database will be compromised via a vulnerability in these additional services.