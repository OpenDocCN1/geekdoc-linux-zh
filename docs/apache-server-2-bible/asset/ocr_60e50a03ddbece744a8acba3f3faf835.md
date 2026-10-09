If you are in a rush to get the certificate to get started with testing or have some other reason why you need a temporary certificate fast, ask your CA. It might have a way to provide you with a temporary, untrusted certificate. For example, Thawte will let you submit your CSR via the Web for a temporary certificate, which you will receive in minutes via e-mail.

After you get the server certificate from a commercial CA, you can install the certificate file per their instructions. This step is usually quite simple. You are likely to be asked to copy the file into a directory and restart the server.

If you are not interested in getting a signed certificate from a commercial CA, you can create your own CA and certify entities such as servers or users at any time. I show you how in the following section.

# # Creating a private certificate authority

As stated earlier, private self-signed certificates are not suitable for Internet use in the sense that users at large should not trust such certificates. However, if you want to be able to issue internal, company-wide certificates to your departments and do not want the hassle of going through the third-party commercial CA verification, you must use a private CA.

**Note**

It might be possible to get a cross-linked certificate for your private CA from a commercial CA. In such a case, your private CA will be chained to the commercial CA and thus everyone should trust any certificate that you issue. However, the commercial CA might limit your certificate-granting authority to your own organization to ensure that you do not compete with the CA.

Follow these steps to create a private self-certified CA using OpenSSL:

+   1.  Download the latest version of the `ssl.ca-version.tar.gz` script distribution from the user-contributed software section (`www.openssl.org/ contrib`) of the OpenSSL Web site. Extract this file to a directory of your choice. A subdirectory called `ssl.ca-version` will be created. You will find a set of `sh` scripts in the directory.

+   2.  Run the `new-root-ca.sh` script to create a self-signed root certificate for your private CA. You will be asked to enter a pass phrase. This pass phrase is required for signing future certificates.

+   3.  To create a server certificate, run the `new-server-cert.sh www.domain.com` script to create a server's private and public key. You will be asked to enter distinguished name fields for the new server certificate. The script will also generate a CSR, which you can send to a commercial CA later if you so choose.

+   4.  Run the `sign-server-cert.sh` script to approve and sign the server certificate you created using the `new-server-cert.sh` script.