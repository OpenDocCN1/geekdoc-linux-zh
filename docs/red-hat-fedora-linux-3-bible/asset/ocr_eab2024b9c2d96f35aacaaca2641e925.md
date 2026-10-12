+   - **make server.csr** — Generates a generic SSL certificate service request.
+   - **make server.crt** — Generates a generic SSL test certificate.
+   - **make stunel.pem** — Generates a generic SSL test certificate, but puts the private key in the same file as the SSL test certificate.
+   - **make genkey** — Same as `make server.key` except it places the key in the `.ssl.key` directory.
+   - **make certreq** — Same as `make server.csr` except it places the certificate service request in the `.ssl.csr` directory.
+   - **make testcert** — Same as `make server.crt` except it places the test certificate in the `.ssl.crt` directory.

# Using third-party certificate signers

In the real world, I know who you are because I recognize your face, your voice, and your mannerisms. On the Internet, I cannot see these things and must rely on a trusted third party to vouch for your identity. To ensure that a certificate is immutable, it has to be signed by a trusted third party when the certificate is issued and validated every time an end user taking advantage of your secure site loads it. The following is a list of the trusted third-party certificate signers:

+   - **GlobalSign** — http://www.globalsign.net/
+   - **GeoTrust** — http://www.geotrust.com/
+   - **VeriSign** — http://www.verisign.com/
+   - **FreeSSL** — http://www.freesll.com/
+   - **Thawte** — http://www.thawte.com/
+   - **En Trust** — http://www.entrust.com/
+   - **ipscA** — http://www.ipsca.com/
+   - **COMODO Group** — http://www.comodogroup.com/

NOTE: Because of the fluid nature of the certificate business, some of these companies may not be in business when you read this, while others may have come into existence. To get a more current list of certificate authorities, use your Mozilla Firefox browser select Edit Preferences. From the Preferences window that appears, select Advanced Manage Certificates. From the Certificate Manager window that appears, refer to the Authorities tab to see Certificate Authorities from which you have received certificates.

Each of these certificate authorities has gotten a chunk of cryptographic code embedded into nearly every Web browser in the world. This chunk of cryptographic code allows a Web browser to determine whether or not an SSL certificate is authentic. Without this validation, it would be trivial for crackers to generate their own certificates and dupe people into thinking they are giving sensitive information to a reputable source.