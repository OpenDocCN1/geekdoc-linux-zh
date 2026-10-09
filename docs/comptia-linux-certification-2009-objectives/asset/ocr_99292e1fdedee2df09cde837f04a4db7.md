key file) -out (Absolute or relative path of certificate request file) to generate a certificate signature request.

+   C. Enter required information such as the country name, state, city, organization name, organizational unit name, server name, email, and if necessary, a challenge password and the optional company name.

+   D. Enter openssl req -new -key {Absolute or relative path of key file} -out {Absolute or relative path of certificate file} -x509 to generate a self-signed certificate.

+   E. Enter required information such as the country name, state, city, organization name, organizational unit name, server name, email, and if necessary, a challenge password and the optional company name.

+   3. Generate digital certificates using the make command.

+   A. Enter make -C /etc/pki/tls/certs {File Name}.key to generate a public or private key pair.

+   B. Enter make -C /etc/pki/tls/certs {File Name}.csr to generate a certificate signature request.

+   C. Enter make -C /etc/pki/tls/certs {File Name}.crt to generate a certificate.

+   D. Enter make -C /etc/pki/tls/certs {File Name}.pem to generate a key and a certificate in one file.