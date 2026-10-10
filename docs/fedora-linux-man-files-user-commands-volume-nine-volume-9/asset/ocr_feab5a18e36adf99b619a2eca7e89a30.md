# ### EXAMPLES

Convert a private from traditional to PKCS#5 v2.0 format using triple DES:
`openssl pkcs8 -in key.pem -topk8 -v2 des3 -out enckey.pem`

Convert a private from traditional to PKCS#5 v2.0 format using AES with 256 bits in CBC mode and **hmacWithSHA256** PRF:
`openssl pkcs8 -in key.pem -topk8 -v2 aes-256-cbc -v2prf hmacWithSHA256 -out enckey.pem`

Convert a private key to PKCS#8 using a PKCS#5 1.5 compatible algorithm (DES):
`openssl pkcs8 -in key.pem -topk8 -out enckey.pem`

Convert a private key to PKCS#8 using a PKCS#12 compatible algorithm (3DES):
`openssl pkcs8 -in key.pem -topk8 -out enckey.pem -v1 PBE-SHA1-3DES`

Read a DER unencrypted PKCS#8 format private key:
`openssl pkcs8 -inform DER -nocrypt -in key.der -out key.pem`

Convert a private key from any PKCS#8 format to traditional format:
`openssl pkcs8 -in pk8.pem -out key.pem`