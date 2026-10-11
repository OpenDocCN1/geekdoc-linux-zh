+   * supported_enctypes is a reference to all the types of encryption supported by the KDC for this realm.

Listing 13.4 shows the complete contents of a typical kdc.conf file.

# ## Listing 13.4 Contents of a typical kdc.conf file

```
```
[ramon]$ more /var/kerberos/krb5kdc/kdc.conf
[kdcdefaults]
  acl_file = /var/kerberos/krb5kdc/kadm5.acl
  dict_file = /usr/dict/words
  admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab

[realms]
  HONTANON.COM = {
    master_key_type = des-cbc-crc
    supported_enctypes = des-cbc-crc:normal des3-cbc-raw:normal
    des3-cbc-sha1:normal des-cbc-crc:v4 des-cbc-crc:afs3
  }
```
```

You may want to create a similar configuration for your KDC. On my server, I also have a DNS alias kerberos.hontanon.com pointing to the IP address of my server, mostly for convenience. This allows me to change the IP address of the server platform, if needed, without having to change the configuration files. I simply make a DNS change for the host name to point to the new address.

# ### The kdb5_util Utility

The kdb5_util utility comes bundled with the Kerberos server package and allows you to perform administrative procedures on the Kerberos authentication database. You can use kdb5_util to create the database, add new principals (humans and machines), and modify and delete those principals.

Let’s start by creating the KDC database with the kdb5_util utility, as shown in Listing 13.5.

# ## Listing 13.5 Creating the KDC database with kdb5_util

```
```
[ramon]$ sudo /usr/kerberos/sbin/kdb5_util create -r HONTANON.COM -s
Initializing database '/var/kerberos/krb5kdc/principal' for realm
'HONTANON.COM',
master key name 'K/M@HONTANON.COM'
You will be prompted for the database Master Password.
It is important that you NOT FORGET this password.
```
```