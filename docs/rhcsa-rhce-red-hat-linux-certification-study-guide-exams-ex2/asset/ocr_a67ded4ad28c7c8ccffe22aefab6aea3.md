3. The /etc/sssd/sssd.conf file should include the following entries:

```
[domain/default]
ldap_id_use_start_tls = False
cache_credentials = True
auth_provider = krb5
debug_level = 0
krb5_kpasswd = maui.example.org
ldap_schema = rfc2307
ldap_search_base = dc=example,dc=org
krb5_realm = EXAMPLE.ORG
chpass_provider = krb5
id_provider = ldap
ldap_uri = ldap://192.168.100.1
krb5_kdcip = maui.example.org
ldap_tls_cacertdir = /etc/openldap/cacerts
```