# CHAPTER 9 | Networked Application Security

# 269

More important, may include authentication methods. For example, the following
TRUST_AUTH_MECH directive lists a list of trusted authentication mechanisms.
TheAUTH_MECHANIS directive lists options offered for authentication. So if these
from the default Het sendmail.mc file are activated, users
who connect to these systems from an MUA client such as Evolution or even Microsoft
Outlook can choose from external Message Digest (MD5) associated with the Java
Cryptography Extension (JCE), MD5 associated with a challenge-response authentication
mechanism (CRAM), regular, or plain-text logics.

```
dml TRUST_AUTH_MECH('EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PAIN') dnl
dnl define('conAUTH_MECHANISMS', 'EXTERNAL GSSAPI-MD5
-CRAM-MD5 LOGIN PAIN') dnl
```

Generally, or plain-text logics should not be used without some encryption.
But that may not be possible with some older MUA clients, such as an older version
of mutt. Fortnormally, several authentication mechanisms are available and configured,
including the generic service application programming interface (GSSAPI)
el as the MD5 options just described.
You may want to create SSL certificates using the private and public key pair
techniques described earlier in this chapter for secure Web sites. The following directives,
elif active, search for needed certificates and keys in the noted files:

```
dml define('confCACERT_PATH', '/etc/pki/tls/certs') dnl
dnl define('confCACERT', '/etc/pki/tls/certs/ca-bundle.crt') dnl
dnl define('confSERVER_CERT',
/etc/pki/tls/certs/sendmail.pem') dnl
dnl define('confSERVER_KEY',
/etc/pki/tls/certs/sendmail.pem') dnl
```

The FEATURE directive includes an exclusive array of options. Some important options
for this directive are listed in Table 9-5.

With the FEATURE directive, avoid specifying the relay_local_from, relay_mail_from,
and accept_unresolvable_domains options, because that can open your system to use by by
spammers. Networks served by the sendmail service can be configured in /etc/mail/access.
In addition, you can take advantage of the /etc/mail/access file to reject e-mails from
the domains of known spammers and black-hat hackers. For more information on anti-spam
features in sendmail, see http://www.sendmail.org/m4/anti_spam.html.

# technical TIP

![](bbox=[0.056, 0.793, 0.944, 0.983])