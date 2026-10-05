# PAM Kerberos

Kerberos to do your authenticating when you log in to your local workstation using CDE, then you must also configure dtlogin to use Kerberos. You configure these services by editing /etc/pam.conf and specifying the PAM Kerberos authentication module /usr/lib/security/pam_krb5.1/ for each. The following is an example for login and ftp:

```
login auth required /usr/lib/security/pam_krb5.1
ftp   auth required /usr/lib/security/pam_krb5.1
```

# 8.3.1.3 /etc/krb5.conf

This file specifies the defaults for the realm and for Kerberos applications, mappings of names onto Kerberos realms, and the location of KDCs for Kerberos realms. A sample /etc/krb5.conf is as follows:

```
[defaults]
  default_realm = REALM.HP.COM
  default_tkt_encypes = DES-CBC-CRC
  default_tgs_encypes = DES-CBC-CRC
  ccache_type = 2

[realms]
  REALM.HP.COM = {
    kdc = hostname.hp.com:88
    admin_server = hostname.hp.com
  }

[domain_realm]
  cup.hp.com = REALM.HP.COM

[logging]
  kdc = FILE:/var/adm/krb5kdc.log
  admin_server = FILE:/var/adm/kadmin.log
  ccache = FILE:/var/adm/krb5lib.log
```

In the environment, of course, you would specify your own realm instead of REALM.HP.COM. In the [defaults] section, you must include "ccache_type = 2" for PAM Kerberos configuration. In the [realms] section, you specify the KDC and administrative server for each realm. You specify the location of log files issued by the KDC and administrative server in the [logging].

# 8.3.1.4 /etc/services

When you install Kerberos, the following entries are automatically placed in your /etc/services-file:

```
#
# Kerberos (Project Athena/MIT) services
#
kerberos5  88/udp  kdc      # Kerberos 5 kdc
klogin     543/tcp             # Kerberos login -kfall
kshell     544/tcp  krcmd   # Kerberos remote shell -kfall
```