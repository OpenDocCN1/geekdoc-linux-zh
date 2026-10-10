
## SEE ALSO

(1)

## PKCS7

### NAME

pkcs7 - PKCS#7 utility

### SYNOPSIS

```
openssl pkcs7 [-inform PEM|DER] [-outform PEM|DER] [-in filename] [-out filename] [-print_certs] [-text] [-noout] [-engine id]
```

### DESCRIPTION

The **pkcs7** command processes PKCS#7 files in DER or PEM format.

### COMMAND OPTIONS

- **-inform DER|PEM**
  This specifies the input format. **DER** format is **DER** encoded **PKCS#7** v1.5 structure. **PEM** (the default) is a base64 encoded version of the **DER** form with header and footer lines.

- **-outform DER|PEM**
  This specifies the output format, the options have the same meaning as the **-inform** option.

- **-in** *filename*
  This specifies the input filename to read from or standard input if this option is not specified.

- **-out** *filename*
  This specifies the output filename to write to or standard output by default.

- **-print_certs**
  Prints out any certificates or CRLs contained in the file. They are preceded by their subject and issuer names in one line format.

- **-text**
  Prints out certificates details in full rather than just subject and issuer names.

- **-noout**
  Don’t output the encoded version of the **PKCS#7** structure (or certificates if **-print_certs** is set).

- **-engine** *id*
  Specifying an engine (by its unique **id** string) will cause **pkcs7** to attempt to obtain a functional reference to the specified engine, thus initialising it if needed. The engine will then be set as the default for all available algorithms.

### EXAMPLES

Convert a PKCS#7 file from PEM to DER:

```
openssl pkcs7 -in file.pem -outform DER -out file.der
```

Output all certificates in a file:

```
openssl pkcs7 -in file.pem -print_certs -out certs.pem
```

### NOTES

The **PEM PKCS#7** format uses the header and footer lines:

```
-----BEGIN PKCS7-----
-----END PKCS7-----
```

For compatibility with some CAs it will also accept:

```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```

### RESTRICTIONS

There is no option to print out all the fields of a PKCS#7 file.

This PKCS#7 routine only understands PKCS#7 v 1.5 as specified in RFC2315; it cannot currently parse, for example, the new CMS as described in RFC2630.

## SEE ALSO

(1)

## PKCS8

### NAME

pkcs8 – PKCS#8 format private key conversion tool

### SYNOPSIS

```
openssl pkcs8 [-topk8] [-inform PEM | DER] [-outform PEM | DER] [-in filename] [-passin arg] [-out filename] [-passout arg] [-noiter] [-nocrypt] [-nooct] [-eed] [-nsdb] [-v2prf alg] [-v1 alg] [-engine id]
```

### DESCRIPTION

The **pkcs8** command processes private keys in PKCS#8 format. It can handle both unencrypted PKCS#8 *PrivateKeyInfo* format and *EncryptedPrivateKeyInfo* format with a variety of PKCS#5 (v1.5 and v2.0) and PKCS#12 algorithms.

### COMMAND OPTIONS

- **-topk8**
  Normally a PKCS#8 private key is expected on input and a traditional format private key will be written. With the **`-topk8`** option the situation is reversed: it reads a traditional format private key and writes a PKCS#8 format key.

- **-inform DER|PEM**
  This specifies the input format. If a PKCS#8 format key is expected on input then either a DER or PEM encoded version of a PKCS#8 key will be expected. Otherwise the DER or PEM format of the traditional format private key is used.

- **-outform DER|PEM**
  This specifies the output format, the options have the same meaning as the **-inform** option.

- **-in** *filename*
  This specifies the input filename to read a key from or standard input if this option is not specified. If the key is encrypted a pass phrase will be prompted for.

- **-passin** *arg*
  The input file password source. For more information about the format of **arg** see the PASS PHRASE ARGUMENTS section in (1).

- **-out** *filename*
  This specifies the output filename to write a key to or standard output by default. If any encryption options are set then a pass phrase will be prompted for. The output filename should **not** be the same as the input filename.

- **-passout** *arg*
  The output file password source. For more information about the format of **arg** see the PASS PHRASE ARGUMENTS section in (1).

- **-nocrypt**
  PKCS#8 keys generated or input are normally PKCS#8 EncryptedPrivateKeyInfo structures using an appropriate password based encryption algorithm. With this option an unencrypted PrivateKeyInfo structure is expected or output. This option does not encrypt private keys at all and should only be used when absolutely necessary. Certain software such as some versions of Java code signing software used unencrypted private keys.

- **-nooct**
  This option generates RSA private keys in a broken format that some software uses. Specifically the private key should be enclosed in an OCTET STRING but some software just includes the structure itself without the surrounding OCTET STRING.

- **-eed**
  This option generates DSA keys in a broken format. The DSA parameters are embedded inside the PrivateKey structure. In this form the OCTET STRING contains an ASN1 SEQUENCE consisting of two structures: a SEQUENCE containing the parameters and an ASN1 INTEGER containing the private key.

- **-nsdb**
  This option generates DSA keys in a broken format compatible with Netscape private key databases. The PrivateKey contains a SEQUENCE consisting of the public and private keys respectively.

- **-v2** *alg*
  This option enables the use of PKCS#5 v2.0 algorithms. Normally PKCS#8 private keys are encrypted with the password based encryption algorithm called **pbeWithMD5AndDES-CBC** this uses 56 bit DES encryption but it was the strongest encryption algorithm supported in PKCS#5 v1.5. Using the **-v2** option PKCS#5 v2.0 algorithms are used which can use any encryption algorithm such as 168 bit triple DES or 128 bit RC2 however not many implementations support PKCS#5 v2.0 yet. If you are just using private keys with OpenSSL then this doesn’t matter.

  The **alg** argument is the encryption algorithm to use, valid values include **des**, **des3** and **rc2**. It is recommended that **des3** is used.

- **-v2prf** *alg*
  This option sets the **PRF** algorithm to use with PKCS#5 v2.0. A typical value would be **hmacWithSHA256**. If this option isn’t set then the default for the cipher is used or **hmacWithSHA1** if there is no default.

- **-v1** *alg*
  This option specifies a PKCS#5 v1.5 or PKCS#12 algorithm to use. A complete list of possible algorithms is included below.

- **-engine** *id*
  Specifying an engine (by its unique **id** string) will cause **pkcs8** to attempt to obtain a functional reference to the specified engine, thus initialising it if needed. The engine will then be set as the default for all available algorithms.

### NOTES

The encrypted form of a PEM encoded PKCS#8 file uses the following headers and footers:

```
-----BEGIN ENCRYPTED PRIVATE KEY-----
-----END ENCRYPTED PRIVATE KEY-----
```

The unencrypted form uses:

```
-----BEGIN PRIVATE KEY-----
-----END PRIVATE KEY-----
```

Private keys encrypted using PKCS#5 v2.0 algorithms and high iteration counts are more secure than those encrypted using the traditional SSLkey compatible formats. So if additional security is considered important the keys should be converted.

The default encryption is only 56 bits because this is the encryption that most current implementations of PKCS#8 will support.

Some software may use PKCS#12 password based encryption algorithms with PKCS#8 format private keys; these are handled automatically but there is no option to produce them.

It is possible to write out DER encoded encrypted private keys in PKCS#8 format because the encryption details are included at an ASN1 level whereas the traditional format includes them at a PEM level.

### PKCS#5 V1.5 AND PKCS#12 ALGORITHMS

Various algorithms can be used with the -v1 command line option, including PKCS#5 v1.5 and PKCS#12. These are described in more detail below.

- PBE-MD2-DES PBE-MD5-DES

  These algorithms were included in the original PKCS#5 v1.5 specification. They only offer 56 bits of protection since they both use DES.

- PBE-SHA1-RC2-64 PBE-MD2-RC2-64 PBE-MD5-RC2-64 PBE-SHA1-DES

  These algorithms are not mentioned in the original PKCS#5 v1.5 specification but they use the same key derivation algorithm and are supported by some software. They are mentioned in PKCS#5 v2.0. They use either 64 bit RC2 or 56 bit DES.

- PBE-SHA1-RC4-128 PBE-SHA1-RC4-40 PBE-SHA1-3DES PBE-SHA1-2DES PBE-SHA1-RC2-128 PBE-SHA1-RC2-40

  These algorithms use the PKCS#12 password based encryption algorithm and allow strong encryption algorithms like triple DES or 128 bit RC2 to be used.
