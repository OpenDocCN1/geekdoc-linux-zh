# 522 Linux Administration: A Beginner's Guide

| Dovecot Config Option | Description |
| --- | --- |
| auth_mechanisms | A list of wanted authentication mechanisms. The authentication types can be broadly categorized into PlainText and Non-plaintext authentication mechanisms. Sample possible values are
- **plain** Most widely supported authentication method, because the client simply sends the password unencrypted (plain text) to Dovecot.
- **login** Usually used by SMTP servers to let e-mail clients perform SMTP authentication. This is also a plain-text mechanism.
- **cram-md5** Protects the password in transit eavesdroppers. Offers good support in clients.
- **ntlm** Suite of authentication and session security protocols created by Microsoft and used in various Microsoft products.
- **anonymous** Provides support for logging in anonymously.|

By default, only the PLAIN mechanism is enabled.

# Table 20-2 Dovecot Configuration Options (Continued)

To get Dovecot up and running quickly, you may have to tweak some configuration parameters at a minimum. The parameters that we will be changing are shown in Table 20-3 along with the desired target values. Table 20-2 explains the meaning of some of these parameters.

# Configure Protocols

Use the doveconf utility to make sure that your server supports LMTP, POP3, and IMAP:

```
[root@server ~]# doveconf protocols
```