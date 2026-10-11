The `ssl_type` enumeration values have the following meanings:

+   • `'` (the empty string) indicates that the account is not required to use secure connections. This is the default value; it’s used when you set up an account but do not specify any `REQUIRE` clause or when you specify `REQUIRE NONE` explicitly.
+   
+   • `'ANY'` indicates that the account must use a secure connection, but that it can be any kind of secure connection; it’s a kind of “generic” requirement. The column is set to this value when you specify `REQUIRE SSL` in a `GRANT` statement.
+   
+   • `'X509'` indicates that the account must use a secure connection and that the client must supply a valid X509 certificate. The contents of the certificate are not otherwise relevant. The column is set to this value when you specify `REQUIRE X509`.
+   
+   • `'SPECIFIED'` indicates that the client must use a secure connection that meets specific requirements. The column is set to this value when you specify any combination of `ISSUER`, `SUBJECT`, or `CIPHER` values in the `REQUIRE` clause.

For all `ssl_type` values except `'SPECIFIED'`, the server ignores the values in the other SSL-related columns when validating client connection attempts. For `'SPECIFIED'`, the server checks the other columns, and for any that have non-empty values, the client must supply matching information:

+   • `ssl_cipher`, if non-empty, indicates the cipher method that the client must use when connecting. It can be used to prevent the client from using weak cipher methods.
+   
+   • `x509_issuer`, if non-empty, indicates the issuer value that must be found in the X509 certificate presented by the client.
+   
+   • `x509_subject`, if non-empty, indicates the subject value that must be found in the X509 certificate presented by the client.

`ssl_cipher`, `x509_issuer`, and `x509_subject` all are represented in the `user` table as `BLOB` columns.

More information about using SSL for secure connections is given later in the chapter, in Section 13.3, “Setting Up Secure Connections.”

# 13.2.1.7 Grant Table Resource Management Columns

The following columns in the `user` table enable you to limit the extent to which any given MySQL account can consume server resources:

+   • `max_connections` indicates the number of times per hour the account can connect to the server. A value of zero means “no limit.” This column has the same name as the `max_connections` system variable, but the two are unrelated.
+   
+   • `max_questions` indicates the number of statements per hour the account can issue. A value of zero means “no limit.”
+   
+   • `max_updates` is like `max_questions`, but applies more specifically to statements that modify data. A value of zero means “no limit.”