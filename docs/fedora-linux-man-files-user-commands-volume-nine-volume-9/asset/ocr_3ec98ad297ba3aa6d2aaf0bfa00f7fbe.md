# STANDARDS

Test vectors from this PKCS#5 v2.0 implentation were posted to the pkcs-tng mailing list using triple DES, DES and RC2 with high iteration counts, several people confird that they could decrypt the private keys produced and Therefore it can be assud that the PKCS#5 v2.0 implentation is reasonably accurate at least as far as these algorihtms are concerned.

The format of PKCS#8 DSA (and other) private keys is not well docunted: it is hidden away in PKCS#11 v2.01, section 11.9. OpenSSL's deaudit DSA PKCS#8 private key format complies with this standard.