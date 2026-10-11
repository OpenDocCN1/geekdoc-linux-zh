# **Table 7.4** *mod_auth_digest* Directives

| Directive | Meaning |
|:--|:--|
| **AuthName** *auth-domain* | Specifies the authentication domain to send the HTTP client. |
| **AuthType** *type* | Specifies the type of password transmission: Basic (in the clear) or Digest (MD5). |
| **AuthDigestDomain** *domain* | One or more URLs that are in the same protection space. |
| **AuthDigestGroupFile** *filename* | Specifies the name of the DB file containing the group authentication information. |
| **AuthDigestFile** *filename* | Specifies the name of the file containing the MD5 digest authentication information. |
| **AuthDBAuthitative** [ on | off ] | Avoid falling back to a lower form of authentication if user is not available. Defaults to on. |

Note that this module uses a digest authentication file (AuthDigestFile) instead of a password file. The digest authentication file is maintained with the htdigest command, and its format is

```
user:password-hash
```

where *user* is the cleartext username, and *password-hash* is the result of the cryptographic hash operation applied on the cleartext password.
An entry in the digest authentication file can also take the form

```
user:realm:MD5-password-hash
```

where *user* is the cleartext username, *realm* is the realm name specified in the **AuthName** directive, and *MD5-password-hash* is the result of the MD5 hashing operation applied on the cleartext password. An example of the **AuthDigestFile** might be:

```
[ramon]$ more .htdigest
alice:private:sd7f90s8dfh0s89df70sdfd0fs8d70sd
bob:private:a8839d9bc0d14b768a14423e1836fec4
charlie:private:sd907fsd09f780sd7f0sdY7f90sydF89
```