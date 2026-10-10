# ## EXAMPLES

Create a cleartext signed ssgae:

```
openssl smi -sign -in ssgae.txt -text -out mail.msg \ -signer mycert.pem
```

Create an opaque signed ssgae:

```
openssl smi -sign -in ssgae.txt -text -out mail.msg -nodetach \ -signer mycert.pem
```

Create a signed ssgae, include so additional certificates and read the private key from another file:

```
openssl smi -sign -in in.txt -text -out mail.msg \ -inkey mycert.pem - inkey mykey.pem -certfile mycerts.pem
```

Create a signed ssgae with two signers:

```
openssl smi -sign -in ssgae.txt -text -out mail.msg \ -signer mycert.pem -signer othercert.pem
```

Send a signed ssgae under Unix directly to sendmail, including headers:

```
openssl smi -sign -in in.txt -text -signer mycert.pem \ -from -to \ -subject "Signed ssgae" | sendmail
```

Verify a ssgae and extract the signer's certificate if successful:

```
openssl smi -verify -in mail.msg -signer user.pem -out signedtext.txt
```

Send encrypted mail using triple DES:

```
openssl smi -encrypt -in in.txt -from \ -to -subject "Encrypted ssgae" \ -des3 user.pem -out mail.msg
```

Sign and encrypt mail:

```
openssl smi -sign -in .txt -signer my.pem -text | openssl smi -encrypt -out mail.msg \ -from -to \ -subject "Signed and Encrypted ssgae" -des3 user.pem
```

Note: the encryption command does not include the **text** option because the ssgae being encrypted already has MIME headers.

Decrypt mail:

```
openssl smi -decrypt -in mail.msg -recip mycert.pem -inkey key.pem
```

The output from Netscape form signing is a PKCS#7 structure with the detached signature format. You can use this program to verify the signature by line wrapping the base64 encoded structure and surrounding it with:

```
-----BEGIN PKCS7-----  -----END PKCS7-----
```

and using the command:

```
openssl smi -verify -inform PEM -in signature.pem -content content.txt
```

Alternatively you can base64 decode the signature and use:

```
openssl smi -verify -inform DER -in signature.der -content content.txt
```