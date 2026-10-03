```
Public key: RSA-CERT SHA256:CfVbRUF+AaUcOxml6wI5Cf5nvtjzBDH6NcXaGU4...
Signing CA: RSA SHA256:CKZFZXRgOy1ji8zmUhU0zjJQFN s9gLEqAwSjA8pB4dg
Key ID: "user_djm"
Serial: 0
Valid: from 2017-12-04T07:31:00 to 2018-12-23T07:32:37
Principals:
djm
Critical Options: (none)
Extensions:
  permit-X11-forwarding
  permit-agent-forwarding
  permit-port-forwarding
  permit-pty
  permit-user-rc
```

While the top looks a whole lot like a host certificate, users get different information below. Our principal is djm, so this certificate is only good for this user. We have no critical options, but the Extensions list several keywords. These are the SSH permissions granted to this user, as we’ll very soon see in “Restricted Certificates.”

Return this certificate to the user.

# Using User Certificates

Copy the certificate into $HOME/.ssh. The user’s public authentication key should already be there.

You should have already set the TrustedUserCAKeys keyword, as discussed in “Trusting your Certificate Authority” earlier this chapter. If so, move the user’s authorized_keys file aside. Have the user SSH into the server. If the server is properly configured, the user should get in without the server having any information about this particular key.

If this is all you want, you’re done. But let’s look at some harder stuff.

# Revoking User Certificates

Generally, you don’t revoke user certificates. You revoke the public keys associated with the certificate, using the RevokedKeys sshd_config keyword.

```
RevokedKeys /etc/ssh/revoked
```

One reason to rotate your CA is that it holds down the length of your revoked certificates list. You don’t want to have certificates from a laptop stolen five years ago still in your revoked certificates file!

If you have a complicated list of revoked keys, investigate Key Revocation Lists (KRLs) in ssh-keygen(8).

# Restricted Certificates

Just as you can limit the access of accounts and keys, you have the power to restrict certificates. You can do this with the -O flag to ssh-keygen. The -O flag has a whole list of possible restrictions identical to those for authorized_keys in Chapter 12. These options include no-agent-forwarding, no-port-forwarding, no-pty, no-user-rc, and no-x11-forwarding. All of these no- restrictions have a corresponding permit-