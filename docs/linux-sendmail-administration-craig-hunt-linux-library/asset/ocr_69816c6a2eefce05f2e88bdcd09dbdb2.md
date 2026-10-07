The tls_client ruleset is called after Sendmail, as a server, receives a STARTTLS command from a remote client. The value in (verify) is checked to see if the TLS handshake completed. The ruleset also looks up (client_name) in the access database using the tag TLS_Clt: If (client_name) (client_addr) is looked up using the tag TLS_Clt: If no entries for the client are found in the access database, the (verify) variable determines whether or not the SMTP connection is allowed. If entries are found, the access database determines whether or not the connection is made.

**Note** Don't remember [client_name] and [client_addr]? They are covered in Chapter 11, "Stamping Spam".

Chapter 6, "Using Sendmail Databases," describes the syntax of the access database including the use of tag fields. In Chapter 6, only three tag fields are described—To:, From;, and Connect:: TLS adds four additional tag fields to the access database syntax—CERTISSUER; SUBJECT; TLS_Clt; and TLS_Srv:: Only access database entries that start with these tags are used for TLS processing. In addition to few new tags, TLS values are added to the access database:

**PERM+|TEMP+VERIFY[:bits]** The VERIFY keyword requires that verification completed successfully—i.e., [verify] must be equal to OK. Optionally, a colon and a number may be added to the keyword. If bits is defined, the encryption key used for this connection must be at least the number of bits is. By default, the verification failure returns a temporary error code, meaning the remote system can retry the connection. Putting the PERM+ in front of the keyword VERIFY causes Sendmail to send a permanent error code. The TEMP+ string causes Sendmail to send a temporary error code, which is the default TLS_PERM_ERROR used in the m4 macro configuration file.

**PERM+|TEMP+ENCR** The ENCR keyword requires that the encryption key used for this must be at least bits number of bits long. Putting the string PERM+ in front of the keyword ENCR cause Sendmail to send a permanent error code. The TEMP+ string causes Sendmail to send a temporary error code, which is the default TLS_PERM_ERROR used in the m4 macro configuration file.

A few sample access database lines will clarify how these are used.

```
TLS_Clt::ibis.foobirds.org              PERM+VERIFY:128
TLS_Srv:wolf.mammals.org               ENCR:128
```

The first line says the connection with a permanent error code if a client named ibis.foobirds.org fails verification or to use a 128-bit encryption key. The second