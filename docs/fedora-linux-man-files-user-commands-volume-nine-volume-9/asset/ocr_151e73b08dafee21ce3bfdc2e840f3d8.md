# OPTIONS

**-accept port**
    The TCP port to listen on for connections. If not specified 4433 is used.

**-context id**
    Sets the SSL context id. It can be given any string value. If this option is not present a default value will be used.

**-cert certna**
    The certificate to use, most servers cipher suites require the use of a certificate and so require a certificate with a certain public key type: for example the DSS cipher suites require a certificate containing a DSS (DSA) key. If not specified then the filena "server.pem" will be used.

**-certform format**
    The certificate format to use: DER or PEM. PEM is the default.

**-key keyfile**
    The private key to use. If not specified then the certificate file will be used.

**-keyform format**
    The private format to use: DER or PEM. PEM is the default.

**-pass arg**
    The private key password source. For more information about the format of **arg** see the PASS PHRASE ARGUMENTS section in (1).

**-dcert filena, -dkey keyna**
    Specify an additional certificate and private key, these behave in the sa manner as the -cert and -key options except there is no default if they are not specified (no additional certificate and key is used). As noted above so cipher suites require a certificate containing a key of a certain type. So cipher suites need a certificate carrying an RSA key and so a DSS (DSA) key. By using RSA and DSS certificates and keys a server can support clients which only support RSA or DSS cipher suites by using an appropriate certificate.

**-dcertform format, -dkeyform format, -dpass arg**
    Additional certificate and private key format and passphrase respectively.

**-nocert**
    If this option is set then no certificate is used. This restricts the cipher suites available to the anonymous ones (currently just anonymous DH).

**-dhlparam filena**
    The DH parater file to use. The epheral DH cipher suites generate keys using a set of DH parsers. If not specified then an attempt is made to load the parsers from the server certificate file. If this fails then a static set of parsers hard coded into the s_server program will be used.

**-no_dhe**
    If this option is set then no DH parsers will be loaded effectively disabling the epheral DH cipher suites.

**-no_tmp_rsa**
    Certain export cipher suites sotis use a temporary RSA key, this option disables