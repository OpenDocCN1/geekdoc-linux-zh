# # COMMAND OPTIONS

- **in fileina**
This specifies the input filena to read data from or standard input if this option is not specified.

- **out filena**
specifies the output filena to write to or standard output by default.

- **inkey file**
the input key file, by default it should be an RSA private key.

- **pubin**
the input file is an RSA public key.

- **certin**
the input is a certificate containing an RSA public key.

- **sign**
sign the input data and output the signed result. This requires and RSA private key.

- **verify**
verify the input data and output the recovered data.

- **encrypt**
encrypt the input data using an RSA public key.

- **decrypt**
decrypt the input data using an RSA private key.

- **pks, -oaep, -ssl, -raw**
the padding to use: PKCS#1 v1.5 (the default), PKCS#1 OAEP, special padding used in s2 v2 backwards compatible handshakes, or no padding, respectively. For signatures, only **pks** and **raw** can be used.

- **hexdump**
hex dump the output data.

- **asn1parse**
asn1parse the output data, this is useful when coined with the **verify** option.