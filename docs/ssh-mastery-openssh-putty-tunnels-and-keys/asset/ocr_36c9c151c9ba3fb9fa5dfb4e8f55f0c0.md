Critical Options: (none)
Extensions: (none)

Perhaps the most vital details here are the key ID (sloth, for the hostname) and the validity dates. If you have multiple certificate authorities, you might find the signing CA field useful. The principals field gives the entities this certificate is valid for, one per line. If you’ve gotten your key files so mixed up that you need to compare the public key field to the keys on your server, start over.

The fields that define critical options and extensions are useful for user certificates.

# User Certificates

User certificates are more complex than host certificates, mainly because users are more complicated than hosts. An SSH user certificate allows you to replicate everything in authorized_keys, including the restrictions and limitations discussed in Chapter 12, “Automation.” This requires delving more deeply into SSH certificates, however.

A key concept of an SSH certificate is the principal. A principal defines what entities this certificate is for. For a host certificate, the principal is the hostname. A user certificate’s principal is usually the username the certificate is for, but it might also contain limitations, restrictions, and other information. A user certificate without a principal can be used to authenticate as any user. You must assign a principal to every certificate, unless you truly want a wildcard authentication certificate.

We’ll refer to the principal throughout this section. Early on you can think of it as the username, but as we proceed the meaning will expand.

# Creating and Viewing User Certificates

Get the user’s public authentication key, usually id_rsa.pub, and copy it to your certificate authority machine. You’ll need it to generate the certificate. The public key is not confidential, so there’s no risk in sending it across the network.

The command to create a user certificate closely resembles creating a host certificate. Use -s to give the path to the user CA key. The -I flag defines the certificate identity, and -n gives the certificate principal. Use -v to define the expiration time. The last argument is the public key file to sign. Here I have my user CA sign the public key of one of my users, making it valid for username djm. I set the validity period to 52 weeks, or one year, because if this expires before the user submits it for renewal I’ll entirely blame it on him.

```
# ssh-keygen -s user-mwlca-key -I user_djm -n djm -V +52w id_rsa.pub
```

I enter the CA passphrase and get a certificate file, id_rsa-cert.pub. If you’ve never done this before, look at the certificate.

```
# ssh-keygen -Lf id_rsa-cert.pub
id_rsa-cert.pub:
    Type: ssh-rsa-cert-v01@openssh.com user certificate
```