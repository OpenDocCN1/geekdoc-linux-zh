Timeout.resolver.retrans.normal=timeout Sets the timeout interval for normal resolver queries.

Timeout.resolver.retry=retries Sets the number of times to retry a resolver query.

Timeout.resolver.retry.first=retries Sets the number of times to retry the first resolver query for a given lookup.

Timeout.resolver.retry.normal=retries Sets the number of times to retry a normal resolver query.

Timeout.rset=timeout Defines how Sendmail will wait for a response to a RSET command.

TimeZoneSpec=tzinfo Sets the local time zone to tzinfo. TimeZoneSpec is not set, the system default is used; if set to null, the user's TZ environment variable is used.

TrustedUser=users Defines the list of users trusted to send mail using another user's name.

TryNullMXlist Causes Sendmail to connect directly to remote hosts that the local system as its preferred MX server, or if the remote host had no MX records.

UnixFromLine=from Defines the format for Unix-style Forms.

UnsafeGroupWrites Prevents Sendmail from allowing group writeable :include and . from files from referencing programs or writing to files. World-writeable files always have these restrictions.

UseErrors Tells Sendmail to return error messages to the addresses listed in the Errors-T header. Normally, errors are sent to the sender address from the envelope.

DatabaseSpec=udbspec Defines the user database specification. Chapter 6. XscriptFileBufferSize=bytes Specifies the amount of buffer memory used for processing an xf queue file.

# Mailer Flags

Mailer flags are declared in the F field of the mailer definition. Each mailer flag is set by a single character that represents that flag. For example, F=1sDFMe sets six different flags. Table C.5 lists the single-character name and function of each flag.