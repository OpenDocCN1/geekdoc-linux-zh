Understanding the role of the S and R rulesets is important when troubleshooting the Sendmail configuration because these rulesets add the variety that is necessary to handle addresses differently for different mailers.

The Argv (A) field defines the mailer command line. It is the argument vector passed to the mailer. It contains, along with the executable command and the command-line arguments, macro expansions that provide the recipient username ($u), the recipient hostname ($h), and the sender's address ($f). These macros are expanded before the argument vector is passed to the mailer.

Maxsize (M) defines, in bytes, the longest message that this mailer will handle, while Limit (L) defines, in bytes, the maximum length of a line that can be contained in a message handled by this mailer. The End-of-line (E) field defines the characters used to mark the end of a line. A newline is the default.

The Directory (D) field specifies the directory for the prog mailer. More than one directory can be specified for the directory field by separating the directory paths with colons: The prog mailer definition in Listing 7.12 uses the recipient's home directory, which is the value returned by the $. If that directory is not available, it then uses the (/).

You can specify the user and the group ID used to execute the mailer with the User (U) field. For example U=mail:mail says that the mailer should be run under the user ID mail and the group ID mail. If no value is specified for the User field, the value defined by the DefaultUser option is used. Note that none of the mailers in Listing 7.12 used the User field.

Nice (N) changes the nice value for the execution of the mailer. This allows you to change the scheduling priority of the mailer. This is rarely used. If you're interested, the nice man page for appropriate values.

The last two fields are used for MIME mail. Charset (C) defines the character set used in the Content-type header when converted to MIME. If Charset is not defined, the value defined by the DefaultCharset option is used. If that option is not defined, unknown-8bit is used as the default value.

The Type (T) field defines the type information used in MIME error messages. MIME type information defines the mailer transfer agent type, the mail address type, and the error code type. The default is dns/rfc8222/smtp.