
Division,0=Thawte Consulting,L=Cape Town,ST=Western Cape,C=ZA""

Alternatively, the -r prints the certificates and then exports them into separate DER binary files. This allows the certificates to be fed to another application that supports .p12 files. Each certificate is written to a sequentially-numbered file, beginning with file0001.der and continuing through file000N.der, incrementing the number for every certificate:

```
pk12util -l test.p12 -r Enter password for PKCS12 file: Key(Shrouded):
Friendly Name: Thawte Freel-mail Meer's Thawte Consulting (Pty) Ltd. ID
Encryption algorithm: PKCS #12 V2 PBE With SHA-1 And 3KEY Triple DES-CBC Parameters: Salt: 45:2e:6a:a0:03:4d:7b:a1:63:3c:15:ea:67:37:62:1f
Iteration Count: 1 (0x1) Certificate Friendly Name: Thawte Personal
Freemail Issuing CA - Thawte Consulting Certificate Friendly Name: Thawte
Freemail Meer's Thawte Consulting (Pty) Ltd. ID
```

## PASSWORD ENCRYPTION

PKCS#12 provides for not only the protection of the private keys but also the certificate and meta-data associated with the keys. Password-based encryption is used to protect private keys on export to a PKCS#12 file and, optionally, the entire package. If no algorithm is specified, the tool defaults to using **PKCS12 V2 PBE with SHA1 and 3KEY Triple DES-cbc** for private key encryption. **PKCS12 V2 PBE with SHA1 and 40 Bit RC4** is the default for the overall package encryption when not in FIPS mode. When in FIPS mode, there is no package encryption.

The private key is always protected with strong encryption by default.
Several types of ciphers are supported.

- Symmetric CBC ciphers for PKCS#5 V2
    - DES-CBC
    - RC2-CBC
    - RC5-CBCPad
    - DES-EDE3-CBC (the default for key encryption)
    - AES-128-CBC
    - AES-192-CBC
    - AES-256-CBC
    - CAMELLIA-128-CBC
    - CAMELLIA-192-CBC
    - CAMELLIA-256-CBC

- PKCS#12 PBE ciphers
    - PKCS #12 PBE with Sha1 and 128 Bit RC4
    - PKCS #12 PBE with Sha1 and 40 Bit RC4
    - PKCS #12 PBE with Sha1 and Triple DES CBC
    - PKCS #12 PBE with Sha1 and 128 Bit RC2 CBC
    - PKCS #12 PBE with Sha1 and 40 Bit RC2 CBC
    - PKCS12 V2 PBE with SHA1 and 128 Bit RC4
    - PKCS12 V2 PBE with SHA1 and 40 Bit RC4 (the default for non-FIPS mode)
    - PKCS12 V2 PBE with SHA1 and 3KEY Triple DES-cbc
    - PKCS12 V2 PBE with SHA1 and 2KEY Triple DES-cbc

- PKCS12 V2 PBE with SHA1 and 128 Bit RC2 CBC
- PKCS12 V2 PBE with SHA1 and 40 Bit RC2 CBC

- PKCS#5 PBE ciphers
    - PKCS #5 Password Based Encryption with MD2 and DES CBC
    - PKCS #5 Password Based Encryption with MD5 and DES CBC
    - PKCS #5 Password Based Encryption with SHA1 and DES CBC

With PKCS#12, the crypto provider may be the soft token module or an external hardware module. If the cryptographic module does not support the requested algorithm, then the next best fit will be selected (usually the default). If no suitable replacement for the desired algorithm can be found, the tool returns the error *no security module can perform the requested operation*.

## NSS DATABASE TYPES

NSS originally used BerkeleyDB databases to store security information. The last versions of these *legacy* databases are:

- cert8.db for certificates
- key3.db for keys
- secmod.db for PKCS #11 module information

BerkeleyDB has performance limitations, though, which prevent it from being easily used by multiple applications simultaneously. NSS has some flexibility that allows applications to use their own, independent database engine while keeping a shared database and working around the access issues. Still, NSS requires more flexibility to provide a truly shared security database.

In 2009, NSS introduced a new set of databases that are SQLite databases rather than BerkeleyDB. These new databases provide more accessibility and performance:

- cert9.db for certificates
- key4.db for keys
- pkcs11.txt, which is a listing of all of the PKCS #11 modules contained in a new subdirectory in the security databases directory

Because the SQLite databases are designed to be shared, these are the *shared* database type. The shared database type is preferred; the legacy format is included for backward compatibility.

By default, the tools (**certutil**, **pk12util**, **modutil**) assume that the given security databases follow the more common legacy type. Using the SQLite databases must be manually specified by using the `sql:` prefix with the given security directory. For example:

```
# pk12util -i /tmp/cert-files/users.p12 -d sql:/home/my/sharednssdb
```

To set the shared database type as the default type for the tools, set the **NSS\_DEFAULT\_DB\_TYPE** environment variable to `sql:`

```bash
export NSS_DEFAULT_DB_TYPE="sql"
```

This line can be added to the `~/.bashrc` file to make the change permanent.

Most applications do not use the shared database by default, but they can be configured to use them. For example, this how-to article covers how to configure Firefox and Thunderbird to use the new shared NSS databases:

For an engineering draft on the changes in the shared NSS databases, see the NSS project wiki:

## SEE ALSO

- certutil (1)
- modutil (1)

The NSS wiki has information on the new database design and how to configure applications to use it.

## ADDITIONAL RESOURCES

For information about NSS and other tools related to NSS (like JSS), check out the NSS project wiki at m[]]. The NSS site relates directly to NSS code changes and releases.

Mailing lists:

IRC: Freenode at #dogtag-pki

## AUTHORS

The NSS tools were written and maintained by developers with Netscape, Red Hat, Sun, Oracle, Mozilla, and Google.

Authors: Elio Maldonado `<>`, Deon Lackey `<>`.

## LICENSE

Licensed under the Mozilla Public License, v. 2.0. If a copy of the MPL was not distributed with this file, You can obtain one at

## NOTES

1. Mozilla NSS bug 836477

## PKACTION

### NAME

pkaction - Get details about a registered action

### SYNOPSIS

```
pkaction [—version] [—help]
pkaction [—verbose]
pkaction —action-id action [—verbose]
```

### DESCRIPTION

**pkaction** is used to obtain information about registered polkit actions. If called without **—action-id** then all actions are displayed. Otherwise the action *action*. If called without the **—verbose** option only the name of the action is shown. Otherwise details about the actions are shown.

### RETURN VALUE

On success **pkaction** returns 0. Otherwise a non-zero value is returned and a diagnostic message is printed on standard error.

### AUTHOR

Written by David Zeuthen <> with a lot of help from many others.

### BUGS

Please send bug reports to either the distribution or the polkit-devel mailing list, see the link m[] on how to subscribe.

### SEE ALSO

(8), (8), (1), (1), (1)

## PKCHECK

### NAME

pkcheck - Check whether a process is authorized

### SYNOPSIS

```
pkcheck [--version] [--help]
pkcheck [--list-temp]
pkcheck [--revoke-temp]
pkcheck --action-id action { --process {pid|pid,pid-start-time|pid,pid-start-time,uid} | --system-bus-name busname } [--allow-user-interaction] [--enable-internal-agent] [--detail key=value...]
```

### DESCRIPTION

**pkcheck** is used to check whether a process, specified by either **—process** (see below) or **—system-bus-name**, is authorized for *action*. The **—detail** option can be used zero or more times to pass details about *action*. If **—allow-user-interaction** is passed, **pkcheck** blocks while waiting for authentication.

The invocation **pkcheck —list-temp** will list all temporary authorizations for the current session and **pkcheck —revoke-temp** will revoke all temporary authorizations for the current session.

This command is a simple wrapper around the polkit D-Bus interface; see the D-Bus interface documentation for details.

### RETURN VALUE

If the specified process is authorized, **pkcheck** exits with a return value of 0. If the authorization result contains any details, these are printed on standard output as key/value pairs using environment style reporting, e.g. first the key followed by an equal sign, then the value followed by a newline.

KEY1=VALUE1 KEY2=VALUE2 KEY3=VALUE3...

Octets that are not in [a-zA-Z0-9\_] are escaped using octal codes prefixed with \ . For example, the UTF-8 string *fōl,你好* will be printed as f\303\270l\54\344\275\240\345\245\275.

If the specified process is not authorized, **pkcheck** exits with a return value of 1 and a diagnostic message is printed on standard error. Details are printed on standard output.

If the specified process is not authorized because no suitable authentication agent is available or if the **—allow-user-interaction** wasn’t passed, **pkcheck** exits with a return value of 2 and a diagnostic message is printed on standard error. Details are printed on standard output.

If the specified process is not authorized because the authentication dialog / request was dismissed by the user, **pkcheck** exits with a return value of 3 and a diagnostic message is printed on standard error. Details are printed on standard output.

If an error occurred while checking for authorization, **pkcheck** exits with a return value of 127 with a diagnostic message printed on standard error.

If one or more of the options passed are malformed, **pkcheck** exits with a return value of 126. If stdin is a tty, then this manual page is also shown.
