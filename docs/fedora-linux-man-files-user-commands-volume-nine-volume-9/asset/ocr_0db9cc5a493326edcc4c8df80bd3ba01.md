# EXAMPLES

Examine and verify certificate request:
`openssl req -in req.pem -text -verify -noout`

Create a private key and then generate a certificate request from it:
`openssl genrsa -out key.pem 1024 openssl req -new -key key.pem -out req.pem`

The sa but just using req:
`openssl req -newkey rsa:1024 -keyout key.pem -out req.pem`

Generate a self signed root certificate:
`openssl req -x509 -newkey rsa:1024 -keyout key.pem -out req.pem`

Example of a file pointed to by the **oid_file** option:
1.2.3.4 shortNa A longer Na 1.2.3.6 otherNa Other longer Na

Example of a section pointed to by **oid_section** making use of variable expansion:
testoid1=1.2.3.5 testoid2=${testoid1}.6

Sample configuration file prompting for field values:
```
[ req ] default_bits = 1024 default_keyfile = privkey.pem distinguished_name = req_distinguished_na attributes = req_attributes x509_extensions = v3_ca
dirstring_type = nobmp [ req_distinguished_na ] countryNa = Country Na (2 letter code) countryNa_default = AU countryNa_min = 2 countryNa_max = 2
localityNa = Locality Na (eg, city) organizationalUnitNa = Organizational Unit Na (eg, section) commonNa = Common Na (eg, YOUR na) commonNa_max = 64
emailAddress = Email Address emailAddress_max = 40 [ req_attributes ]
challengePassword = A challenge password challengePassword_min = 4
challengePassword_max = 20 [ v3_ca ] subjectKeyIdentifier=hash
authorityKeyIdentifier=keyid:always, issuer:always basicConstraints = CA:true
```

Sample configuration containing all field values:
```
RANDFILE = $ENV::HOME/.rnd [ req ] default_bits = 1024 default_keyfile = keyfile.pem distinguished_na = req_distinguished_na attributes = req_attributes prompt = no output_password = mypass [ req_distinguished_na ]
C = GB ST = Test State or Province L = Test Locality O = Organization Na OU = Organizational Unit Na CN = Common Na emailAddress = [ req_attributes ]
challengePassword = A challenge password
```