
Where *id* is the ID of the cryptographic engine. To check the availability of an engine, issue the following command:

```bash
~]$ openssl engine -t
```

To sign a data file called *plaintext*, issue a command as follows:

```bash
~]$ openssl pkeyutl -sign -in plaintext -out sigtext -inkey privkey.pem
```

To verify a signed data file and to extract the data, issue a command as follows:

```bash
~]$ openssl pkeyutl -verifyrecover -in sig -inkey key.pem
```

To verify the signature, for example using a DSA key, issue a command as follows:

```bash
~]$ openssl pkeyutl -verify -in file -sigfile sig -inkey key.pem
```

The pkeyutl(1) manual page describes the public key algorithm utility.

### Using Symmetric Algorithms

To list available symmetric encryption algorithms, execute the enc command with an unsupported option, such as -l:

```bash
~]$ openssl enc -l
```

To specify an algorithm, use its name as an option. For example, to use the **aes-128-cbc** algorithm, use the following syntax:

```bash
openssl enc -aes-128-cbc
```

To encrypt a file called **plaintext** using the **aes-128-cbc** algorithm, enter the following command:

```bash
~]$ openssl enc -aes-128-cbc -in plaintext -out plaintext.aes-128-cbc
```

To decrypt the file obtained in the previous example, use the **-d** option as in the following example:

```bash
~]$ openssl enc -aes-128-cbc -d -in plaintext.aes-128-cbc -out plaintext
```

> ### **IMPORTANT**
>
> The enc command does not properly support AEAD ciphers, and the ecb mode is not considered secure. For best results, do not use other modes than cbc, cfb, ofb, or ctr.

### 4.7.5. Generating Message Digests

The dgst command produces the message digest of a supplied file or files in hexadecimal form. The command can also be used for digital signing and verification. The message digest command takes the following form:

```bash
openssl dgst algorithm -out filename -sign private-key
```

Where *algorithm* is one of `md5|md4|md2|sha1|sha|mdc2|ripemd160|dss1`. At time of writing, the SHA1 algorithm is preferred. If you need to sign or verify using DSA, then the *dss1* option must be used together with a file containing random data specified by the `-rand` option.

To produce a message digest in the default Hex format using the *sha1* algorithm, issue the following command:

```bash
~]$ openssl dgst sha1 -out digest-file
```

To digitally sign the digest, using a private key *prikey.pem*, issue the following command:

```bash
~]$ openssl dgst sha1 -out digest-file -sign prikey.pem
```

See man dgst(1) for more information.

### 4.7.6. Generating Password Hashes

The *passwd* command computes the hash of a password. To compute the hash of a password on the command line, issue a command as follows:

```bash
~]$ openssl passwd password
```

The `-crypt` algorithm is used by default.

To compute the hash of a password from standard input, using the MD5 based BSD algorithm *-1*, issue a command as follows:

```bash
~]$ openssl passwd -1 password
```

The *-apr1* option specifies the Apache variant of the BSD algorithm.

To compute the hash of a password stored in a file, and using a salt *xx*, issue a command as follows:

```bash
~]$ openssl passwd -salt xx -in password-file
```

The *password* is sent to standard output and there is no *-out* option to specify an output file. The `-table` will generate a table of password hashes with their corresponding clear text password.

See man sspasswd(1) for more information and examples.

### 4.7.7. Generating Random Data

To generate a file containing random data, using a seed file, issue the following command:

```bash
~]$ openssl rand -out rand-file -rand seed-file
```

Multiple files for seeding the random data process can be specified using the colon, `:`, as a list separator.

See man rand(1) for more information.

### 4.7.8. Benchmarking Your System

To test the computational speed of a system for a given algorithm, issue a command in the following format:

```bash
openssl speed algorithm
```

where algorithm is one of the supported algorithms you intended to use. To list the available algorithms, type openssl speed and then press tab.

### 4.7.9. Configuring OpenSSL

OpenSSL has a configuration file /etc/pki/tls/openssl.cnf, referred to as the master configuration file, which is read by the OpenSSL library. It is also possible to have individual configuration files for each application. The configuration file contains a number of sections with section names as follows: [ section_name ]. Note the first part of the file, up until the first [ section_name ], is referred to as the default section. When OpenSSL is searching for names in the configuration file the named sections are searched first. All OpenSSL commands use the master OpenSSL configuration file unless an option is used in the command to specify an alternative configuration file. The configuration file is explained in detail in the config(5) man page.

Two RFCs explain the contents of a certificate file. They are:

- Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) Profile
- Updates to the Internet X.509 Public Key Infrastructure Certificate and Certificate Revocation List (CRL) Profile

## 4.8. USING STUNNEL

The stunnel program is an encryption wrapper between a client and a server. It listens on the port specified in its configuration file, encrypts the communication with the client, and forwards the data to the original daemon listening on its usual port. This way, you can secure any service that itself does not support any type of encryption, or improve the security of a service that uses a type of encryption that you want to avoid for security reasons, such as SSL versions 2 and 3, affected by the POODLE SSL vulnerability (CVE-2014-3566). See https://access.redhat.com/solutions/1234773 for details. CUPS is an example of a component that does not provide a way to disable SSL in its own configuration.

### 4.8.1. Installing stunnel

Install the stunnel package by entering the following command as root:

```bash
# yum install stunnel
```

### 4.8.2. Configuring stunnel as a TLS Wrapper

To configure stunnel, follow these steps:

- You need a valid certificate for stunnel regardless of what service you use it with. If you do not have a suitable certificate, you can apply to a Certificate Authority to obtain one, or you can create a self-signed certificate.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_102_0.png)

# WARNING

Always use certificates signed by a Certificate Authority for servers running in a production environment. Self-signed certificates are only appropriate for testing purposes or private networks.

See *Section 4.7.2.1, “Creating a Certificate Signing Request”* for more information about certificates granted by a Certificate Authority. On the other hand, to create a self-signed certificate for stunnel, enter the `/etc/pki/tls/certs/` directory and type the following command as *root*:

```bash
certs]# make stunnel.pem
```

Answer all of the questions to complete the process.

- 2. When you have a certificate, create a configuration file for stunnel. It is a text file in which every line specifies an option or the beginning of a service definition. You can also keep comments and empty lines in the file to improve its legibility, where comments start with a semicolon.

The stunnel RPM package contains the `/etc/stunnel/` directory, in which you can store the configuration file. Although stunnel does not require any special format of the file name or its extension, use `/etc/stunnel/stunnel.conf`. The following content configures *stunnel* as a TLS wrapper:

```ini
cert = /etc/pki/tls/certs/stunnel.pem
; Allow only TLS, thus avoiding SSL
sslVersion = TLSv1
chroot = /var/run/stunnel
setuid = nobody
setgid = nobody
pid = /stunnel.pid
socket = l:TCP_NODELAY=1
socket = r:TCP_NODELAY=1

[service_name]
accept = port
connect = port
TIMEOUTclose = 0
```

Alternatively, you can avoid SSL by replacing the line containing `sslVersion = TLSv1` with the following lines:

```ini
options = NO_SSLv2
options = NO_SSLv3
```

The purpose of the options is as follows:

- cert – the path to your certificate
