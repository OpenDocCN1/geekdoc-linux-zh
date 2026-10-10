sure there is a newline character at the end of the last line. Then run signtool with standard input redirected from your file as follows:

```
signtool -G MyTestCert inputfile
```

The prompts show up on the screen, but the responses will be automatically read from the file. The password will still be read from the console unless you use the -p option to give the password on the command line.

# Using the -M Option to List Smart Cards

You can use the -M option to list the PKCS #11 modules, including smart cards, that are available to signtool:

```
signtool -d "c:\netscape\users\jsmith" -M using certificate directory:
c:\netscape\users\usern a Listing of PKCS11 modules --------------------------
--------------------------- 1. Netscape Internal PKCS #11 Module (this
module is internally loaded) slots: 2 slots attached status: loaded
slot: Commticor Internal Cryptographic Services Version 4.0 token:
Commicator Generie Crypto Svcs slot: Commicator User Private Key and
Certifiate Services token: Commicator Certificate DB 2. CryptoS (this
is an external module) DLL na: core32 slots: 1 slots attached status:
loaded slot: Litronic 210 token: --- ---- ---- ---- ---- ---- ---- ---
---- ---- ---- ---- ---- ---- ----
```

# Using Netscape Signing Tool and a Smart Card to Sign Files

The signtool command normally takes an argument of the -k option to specify a signing certificate. To sign with a smart card, you supply only the fully qualified na of the certificate.

To see fully qualified certificate nas when you run Commicator, click the Security button in Navigator, then click Yours under Certificates in the left fra. Fully qualified nas are of the format smart card:certificate, for example "MyCard:My Signing Cert". You use this na with the -k argument as follows:

```
signtool -k "MyCard:My Signing Cert" directory
```

# Verifying FIPS Mode

Use the -M option to verify that you are using the FIPS-140-1 module.

```
signtool -d "c:\netscape\users\jsmith" -M using certificate directory:
c:\netscape\users\jsmith Listing of PKCS11 modules ---------------------
--------------------------- 1. Netscape Internal PKCS #11 Module (this
module is internally loaded) slots: 2 slots attached status: loaded
slot: Commticor Internal Cryptographic Services Version 4.0 token:
Commicator Generie Crypto Svcs slot: Commicator User Private Key and
Certifiate Services token: Commicator Certificate DB -------------------
------ ----
```

This Unix example shows that Netscape Signing Tool is using a FIPS-140-1 module: