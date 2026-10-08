# praliases

aliases, one per line, in no particular order. The form is key: value. When you specify a key, only that key is looked up and the appropriate key: value is displayed if found.

# Options

+   -c configfile

Specify a sendmail configuration file.

+   -f aliasfile

Reads the specified file aliasfile instead of the default sendmail system aliases file.

# Operands

+   key

A specific key to look up.

# Exit Status

+   0

+   >0

Successful operation.

An error occurred.

# Files

+   /etc/mail/sendmail.cf

The default sendmail configuration file.

+   /etc/mail/aliases

The default sendmail system aliases file.

+   /etc/mail/aliases.dir

+   /etc/mail/aliases.pag

The database versions of the /etc/mail/aliases.file.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwisndmu |

# See Also

mailq(1), newaliases(1), sendmail(1M), attributes(5)