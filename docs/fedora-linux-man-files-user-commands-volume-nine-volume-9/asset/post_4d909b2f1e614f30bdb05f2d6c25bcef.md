
This allows an alternative configuration file to be specified. This overrides the compile-time file or any specified in the `OPENSSL_CONF` environment variable.

### **-subj arg**

Sets subject name for new request or supersedes the subject name when processing a request. The arg must be formatted as `/type0=value0/type1=value1/type2=...`. Characters may be escaped by `\` (backslash), no spaces are skipped.

### **-multivalue-rdn**

This option causes the `-subj` argument to be interpreted with full support for multi-valued RDNs. Example:

```
/DC=org/DC=OpenSSL/DC=users/UID=123456+CN=John Doe
```

If `-multivalue-rdn` is not used, then the UID value is `123456+CN=John Doe`.

### **-x509**

This option outputs a self-signed certificate instead of a certificate request. This is typically used to generate a test certificate or a self-signed root CA. The extensions added to the certificate (if any) are specified in the configuration file. Unless specified using the **set_serial** option, a large random number will be used for the serial number.

### **-days n**

When the **-x509** option is being used, this specifies the number of days to certify the certificate for. The default is 30 days.

### **-set_serial n**

Serial number to use when outputting a self-signed certificate. This may be specified as a decimal value or a hex value if preceded by **0x**. It is possible to use negative serial numbers but this is not recommended.

### **-extensions section**

### **-reqexts section**

These options specify alternative sections to include certificate extensions (if the **-x509** option is present) or certificate request extensions. This allows several different sections to be used in the same configuration file to specify requests for a variety of purposes.

### **-utf8**

This option causes field values to be interpreted as UTF8 strings. By default, they are interpreted as ASCII. This means that the field values, whether prompted from a terminal or obtained from a configuration file, must be valid UTF8 strings.

### **-nameopt option**

Option which determines how the subject or issuer names are displayed. The **option** argument can be a single option or multiple options separated by commas. Alternatively, the **-nameopt** switch may be used more than once to set multiple options. See the (1) manual page for details.

### **-reqopt option**

Customise the output format used with **-text**. The **option** argument can be a single option or multiple options separated by commas.

See discussion of the `-certopt` parameter in the `x509` command.

- **-asn1-kludge**: By default, the **req** command outputs certificate requests containing no attributes in the correct **PKCS#10** format. However, certain CAs will only accept requests containing no attributes in an invalid form; this option produces this invalid format.

More precisely, the **Attributes** in a **PKCS#10** certificate request are defined as a **SET OF Attribute**. They are **not OPTIONAL**, so if no attributes are present, then they should be encoded as an empty **SET OF**. The invalid form does not include the empty **SET OF**, whereas the correct form does.

It should be noted that very few CAs still require the use of this option.

- **-no-asn1-kludge**: Reverses effect of **-asn1-kludge**.

- **-newhdr**: Adds the word **NEW** to the **PEM** file header and footer lines on the outputted request. So software (Netscape certificate server) and some CAs need this.

- **-batch**: Non-interactive mode.

- **-verbose**: Print extra details about the operations being performed.

- **-engine id**: Specifying an engine (by its unique **id** string) will cause **req** to attempt to obtain a functional reference to the specified engine, thus initialising it if needed. The engine will then be set as the default for all available algorithms.

- **-keygen_engine id**: Specifies an engine (by its unique **id** string) which would be used for key generation operations.

## CONFIGURATION FILE FORMAT

The configuration options are specified in the **req** section of the configuration file. As with all configuration files, if no value is specified in the specific section (i.e. **req**), then the initial unnamed or **default** section is searched too.

The options available are described in detail below.

- **input_password output_password**

The passwords for the input private key file (if present) and the output private key file (if one will be created). The command line options **passin** and **passout** override the configuration file values.

- **default_bits**

This specifies the default key size in bits. If not specified, then 512 is used. It is used if the **-new** option is used. It can be overridden by using the **-newkey** option.

- **default_keyfile**

This is the default filename to write a private key to. If not specified, the key is written to standard output. This can be overridden by the **-keyout** option.

- **oid_file**

This specifies a file containing additional **OBJECT IDENTIFIERS**. Each line of the file should consist of the numerical form of the object identifier followed by white space, then the short name followed by white space, and finally the long name.

- **oid_section**

This specifies a section in the configuration file containing extra object identifiers. Each line should consist of the short name of the object identifier followed by `=` and the numerical form. The short and long names are the same when this option is used.

- **RANDFILE**

This specifies a filename in which random number seed information is placed and read from, or an EGD socket (see `RAND_egd(3)`). It is used for private key generation.

- **encrypt_key**

If this is set to **no**, then if a private key is generated, it is **not** encrypted. This is equivalent to the **-nodes** command line option. For compatibility, **encrypt_rsa_key** is an equivalent option.

- **default_md**

This option specifies the digest algorithm to use. Possible values include **md5**, **sha1**, **mdc2**. If not present, then **MD5** is used. This option can be overridden on the command line.

- **string_mask**

This option masks out the use of certain string types in certain fields. Most users will not need to change this option.

It can be set to several values:
- **default** (which is also the default option) uses PrintableStrings, T61Strings and BMPStrings.
- If the **pkix** value is used, then only PrintableStrings and BMPStrings will be used. This follows the **PKIX** recommendation in RFC2459.
- If the **utf8only** option is used, then only UTF8Strings will be used; this is the PKIX recommendation in RFC2459 after 2003.
- Finally, the **nostr** option just uses PrintableStrings and T61Strings: certain software has problems with BMPStrings and UTF8Strings; in particular, Netscape.

### req_extensions

This specifies the configuration file section containing a list of extensions to add to the certificate request. It can be overridden by the **-reqexts** command line switch. See the (5) manual page for details of the extension section format.

### x509_extensions

This specifies the configuration file section containing a list of extensions to add to the certificate generated when the **-x509** switch is used. It can be overridden by the **-extensions** command line switch.

### prompt

If set to the value **no**, this disables prompting of certificate fields and just takes values from the config file directly. It also changes the expected format of the **distinguished_name** and **attributes** sections.

### utf8

If set to the value **yes**, then field values are interpreted as UTF8 strings. By default, they are interpreted as ASCII. This means that the field values, whether prompted from a terminal or obtained from a configuration file, must be valid UTF8 strings.

### attributes

This specifies the section containing any request attributes: its format is the same as **distinguished_name**. Typically, these may contain the `challengePassword` or `unstructuredName` types. They are currently ignored by OpenSSL’s request signing utilities, but some CAs might want them.

### distinguished_name

This specifies the section containing the distinguished name fields to prompt for when generating a certificate or certificate request. The format is described in the next section.
