TLSA-type DNS record. But be careful: Every time you change the SSL certificate in the future, you also have to remember to update your own DANE record. Mail servers with a state-of-art configuration like Postfix will stop outgoing mail if the certificate and fingerprint published via DANE do not match or if a target does not offer SSL/TLS even though a DANE/TLSA record has been published. The `main.cf` file of the sending mail server needs a `smtpls_security_level = dane line, even if the server does not offer DANE for incoming messages.

# Securing the Contents

SSL is in place. Is everything fine? Not at all, because SSL only secures the TCP/IP connection between two specific mail servers. No one knows whether the message might be transmitted over unencrypted connections further down the line. In addition, the email itself ends up in plaintext on the servers, both in the recipient’s inbox and in the sender’s Sent folder.

An electronic mailbox that has operated for years, perhaps even decades, many highly personal things could exist that you would probably prefer to keep out of the public eye. Every user needs to ask what impact it would have if their entire email inbox became public, because that can happen all too quickly. A poorly chosen IMAP password can be easily hacked; it may have even been revealed in an inattentive moment to a phishing site or intercepted by a local virus infection.

The only way to ensure that your email will remain private is to encrypt the messages using PGP or S/MIME. Both methods are based on the same principle: Each user has an asymmetric key pair. It consists of a public key, which is used for encryption and a digital signature, and a private key, which is used for decryption and verification of a digital signature. A password chosen by the user protects the private key against unauthorized access. This password must not be forgotten under any circumstances. If it is lost, the key file is unusable, and all data encrypted with it can no longer be accessed.

# Pretty Good Privacy

Many Linux users today are accustomed to working with PGP. You store your own public key, together with those of other recipients in a local key database, also known as a keyring. Since several keys can be generated for a mail address over time, each key has its own ID. In addition, the authenticity of a key can be verified using a mathematically unique fingerprint. This fingerprint can be published on business cards or in your web imprint or verified by phone, which allows communication partners to ensure that they really have the right key.

Generating a public/private key pair is quite simple nowadays and usually occurs automatically the first time you use the PGP software tool. The public key can then be transmitted individually or automatically to communication partners. Mail programs such as Thunderbird offer to attach the public key to an

outgoing email at the push of a button. You can also upload the public key to public PGP key servers, where interested parties will find it automatically.

Once a key has been put into circulation, it can no longer be deleted, but it can be declared invalid in the event of key theft or password loss. To declare a key invalid, you should generate a revoke certificate ahead of time (i.e., immediately after generating the key) and store it in a secure place in your own filesystem. If your own password is lost, you no longer have the option of creating a revoke certificate. In addition, keys should not be issued for an indefinite period of time but assigned an expiration date a few years in the future.

All of these options are usually found in the mail program’s key manager. Press the right mouse button to call up the properties and potential actions for your own key (Figure 1).

One problem remains: It is initially impossible to verify whether a key actually originates from the owner of the mail address. Attackers can easily generate their own PGP keys for any mail address and put them into circulation. The public PGP keys of other users are therefore initially considered untrustworthy in your own keyring. However, the sender and recipient can have the specific PGP fingerprint displayed there and verify it via another communication medium – by making a short phone call if necessary.

So much for the theory. In practice, many users today use the keys they receive without verification. In the settings of most popular mail programs, you can define the trust level from which a key can be used for sending. This is certainly not ideal and could convey a deceptive sense of security. On the other hand, using any kind of encryption is better than having none at all, so in the interest of the matter at hand, just take a pragmatic approach if in doubt. A received key is insecure if it has been manipulated by a third party at the time of receipt and the compromised key is trusted permanently. But if you assume that the key exchange (which may have occurred long ago) was secure at the time, the key can successfully provide protection against future unwanted readers and the dreaded man in the middle.

![](bbox=[0.35, 0.65, 0.93, 0.9])