# Part III: Administering Fedora and RHEL

A challenge password [:
An optional company name []:

# Getting the CSR signed

Once your CSR has been created, you will need to sign a signing authority for validation. The first step is to select a signing authority. Each signing authority has different deals, prices, and products. Check each of the signing authorities listed in the “Using thirdparty certificate signers” earlier in this chapter to determine which works best for you. The following are where signing authorities differ:

+   * Credibility and stability
* Pricing
* Browser recognition
* Warranties
* Support
* Certificate strength

After you have selected your signer, you will need to go through some validation steps. Each signer has a different method of validating identity and certificate information. Others may require that you provide a company officer to be made available to a validation operator. At the point in which you will need to copy and paste the CSR you created into your signer’s Web form.

```
# cat /etc/pki/tls/certs
# cat localhost.csr
-- BEGIN CERTIFICATE REQUEST -
MIBB6JCCVAMCAQagkwkZAQBNGVAYAT1lMRQwEgYDVQQQIEtdb25zuZNW0aWN1
DEPEPMAGAgUBeXMTX3lJJMRowXBgGVDVQQQFXBY211IEhlcm1uSwgWS5J5lJER
M8GA11EMcXWMISb1b1Ry2Q2gAgVNBtEnd5y3j211bfYWa5h5lmWNbTen
QMCUCGSG33DbAg2QYJARDYVvRIB3W65fJgBv0Y2JtYYbpEu29Y7MIGFMAOGCSQG
uU2c2b6iY4wHAtdXubAbD/Y/M12QYX6M4444PFl135E50QfY2tcZlyC4444444444444444444444444444444444444p3YpTCmC4
gBwwW1DAQBoAQABoYQKJ3hccNAQEDAgQYVVeoJAJJZgpnR5H2Y9R9Wg
18o1B3gG60c3pW4p0bQg708s/++QQZ2WI11efgaQSMInKII77FS
YIWYbpPoTMC4C4b0pTZTURCYQRGKXbW7bI/A35nvkR77yqN9lq7681FEJ8
W9J3PX4vb2+ntcbi-
-- END CERTIFICATE REQUEST --
```

You can use your mouse to copy and paste the CSR into the signer’s Web form.

After you have completed the information validation, for the signing, and all of the questions, you have completed most of the process. In 48 to 72 hours you should receive an email with your new shiny SSL certificate in it. This certificate will look similar to the following: