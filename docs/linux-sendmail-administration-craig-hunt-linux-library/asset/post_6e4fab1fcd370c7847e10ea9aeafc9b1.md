
# Securing a Sendmail Server

in a recipient address to forward mail to a program. You do not define the .forward file for every user, but as the Sendmail administrator you are responsible for the contents of the aliases database.

Make sure that no one can modify the aliases database. The aliases file and the directory that contains the aliases file should only be writable by the owner, who is the Trusteduser (usually root). If you put an alias in the database that sends mail to a program, you must be absolutely sure that the program you send the mail to handles the data properly. Buffer overflows and other data-handling problems are a big security hole commonly exploited by intruders. Personally, I never mail to a program.

You might not be able to create the .forward file for every user, but you can control the programs that are available to the user through the I program syntax. Controlling these programs is the primary function of smrf.

# Using the smrf Feature

The smrf feature was introduced during the discussion of the Red Hat configuration in Chapter 5, “Understanding a Vendor's Configuration.” smrf is the Sendmail Restricted Shell. It replaces /bin/sh as the program used for the prolog mail. The prolog mail is the mail delivery agent used when Sendmail processes an address that uses the I program syntax. On Linux systems /bin/sh is the Bourne Shell (bash), which means that any command that can be processed by bash can process the prolog mail is a very flexible but a potentially dangerous one. Anyone who can get a command to the prolog mail has same access to the system as a user logged on a terminal. smrf limits the flexibility and reduces the danger.

smrf is a restricted shell. Built-in shell commands--exec, exit, and echo--work, but most do not. smrf does not allow standard IO redirection. Most of the characters used by the shell--carriage return, newline, <, >, ;, $, and ()-are not allowed; only ll and && are accepted. Most importantly, only those commands that can be run by exec or those that you choose to make available to smrf through a special execution are available to the user.

smrf forwards only to programs in the /usr/adm/sm.bin directory. The Sendmail administrator creates the /usr/adm/sm.bin directory and populates it with the programs that are to be accessible through the prolog mail. smrf strips the pathname off of the program to which mail is being forwarded. Thus, if the user enters /usr/local/vacation as the program name, smrf strips the program name down and looks for a file of that name in the /usr/adm/sm.bin directory.

/usr/adm/sm.bin is the default execution directory by smrf. Compile smrf with either the -DPATH -DCMDBIN compile options to specify a different execution path.

![](img/9639113aa446fb8976cb3d377f7aafdd_364_0.png)

execution path is often changed on Linux systems. For example, Red Hat defines the path as /etc/smrsh, programs trained to receive forwarded mail are stored in the /etc/smrsh directory.

Take care when adding programs to the smrsh execution directory. Poorly written programs are popular targets for attackers. Every program is a potential hole for an intruder to exploit. Choose them carefully.

# Sendmail Security Protocols

The first two sections of this chapter cover techniques for securing a Sendmail server. None of the things you do to make your server more secure can ensure the security of mail as it moves through the network. Mail can be corrupted or read at any point as it travels through the network. No one can have a reasonable expectation of privacy with e-mail. It is cleartext moving through a shared network. Everyone knows that their e-mail is an open communication shared to the world.

Sometimes, however, you want to keep your mail private. This can be done using add-on tools, such as Pretty Good Privacy (PGP) or Gnu Privacy Guard (GnPG), to secure messages. These tools, are not integrated into Sendmail. Starting with Sendmail 8.11, some standard Internet security protocols have been added to Sendmail to authenticate clients and secure connections. Four basic protocols have been added to Sendmail to support secure mail messages:

- STARTTLS RFC 2487 ("SMTP Service Extension for Secure SMTP over TLS") defines the STARTTLS protocol that standardizes the transmission of encrypted e-mail. STARTTLS depends on transport layer security (TLS).
- TLS RFC 2246 ("The TLS Protocol Version 1.0") defines a protocol that provides encrypted communications between two applications, such as two message agent (MTA) programs. TLS is based on Sockets Layer (SSL). SSL is the security mechanism used for e-commerce on the Web. TLS and SSL have different, but the TLS RFC allows for compatibility with SSL. Sendmail takes advantage of this and uses SSL for its transport layer security.
- AUTH RFC 2554 ("SMTP Service Extension for Authentication") defines the AUTH protocol that is used to authenticate the end points in an e-mail exchange. AUTH depends on the Simple Authentication and Security Layer (SASL).
- SASL RFC 2222 ("Simple Authentication and Security Layer (SASL)") defines a generalized method for adding authentication to connection-oriented protocols, such as SMTP.

# Sendmail Security Protocols

Sendmail implements the AUTH protocol and the STARTTLS protocol, but it depends on Linux for TLS and SASL. We saw this dependency in Chapter 3, “Running Sendmail,” when we attempted to install the RPM version of Sendmail 8.11 on a Linux system that did not have SSL or SASL installed. RPM complained that Sendmail 8.11 depended on openssl and libsasl and neither was provided. It is the convergence of cryptographic support in the operating system and Sendmail that makes it possible for your server to secure e-mail.

The Sendmail security protocols ensure the authenticity of MTAs and the integrity of e-mail in the network. To accomplish these tasks, the protocols use cryptography to authenticate and secure SMTP communications. This isn’t a book about cryptography; however, some cryptographic concepts are essential for understanding the Sendmail security protocols.

# Encryption and Cryptography

There are two basic types of cryptography: secret key, which is also called symmetric cryptography, and public key, which is sometimes asymmetric cryptography. Symmetric cryptography is easy to understand. Cooperating systems use the same key and the same algorithm to encrypt and decrypt data. The problem with symmetric cryptography is that a prior agreement must be reached among all participating systems about the key and the algorithm to be used. The secret key in a secret key system is far from being a secret because every system must have a copy of the key. The more systems sharing the secret, the greater the possibility that it will be compromised.

Public cryptography is a much more interesting system. It uses two keys—a public key that can be available to everyone and a private key that does not need to be shared with anyone. When the public key is used to encrypt a message, the message can be decrypted only with the private key. Thus, anyone can encrypt a message for the target system using the public key, but only the target system can decrypt and read the message using its private key. Importantly, only messages encrypted with the private key can be decrypted with the public key. This elegant system is not without complexity. Two things are required to make it work:

Authentication In a secret cryptography system, the fact that a message is properly encrypted means that it must have come from a trusted system that has the secret key. A public key is different. Because the public key is available to everyone, a method for authenticating the source of an encrypted message is needed. Messages are authenticated by a digital signature. A digital signature is produced by running a cryptographic checksum using the content of the message as the data for the checksum and the private key of the source of the message for the encryption. Since the digital signature was produced with the source’s private key, it can only be

![](img/9639113aa446fb8976cb3d377f7aafdd_366_0.png)
