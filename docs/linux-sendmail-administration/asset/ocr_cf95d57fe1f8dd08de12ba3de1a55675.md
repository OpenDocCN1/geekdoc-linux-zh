SevenBitInput Causes Sendmail to strip input to seven bits for compatibility with old systems. This shouldn't be necessary.

SingleLineFromHeader For compatibility with some versions of Lotus Notes, causes Sendmail to unwrap From: lines that have embedded newlines into one line.

SingleThreadDelivery Tells Sendmail not to open more than one SMTP connection to a remote host at the same time. This option works only if the option HostStatusDirectory is also specified.

SmtpGreetingMessage defines the greeting sent to the remote host when it connects to the SMTP server port.

StatusFile Tells Sendmail to log summary statistics in the specified file. By default, summary statistics are not logged.

SuperSafe Tells Sendmail to create a queue file for every piece of mail, when attempting immediate delivery.

TempfileMode=mode sets the access permissions for queue files. mode is an octal value. Default to 0600.

Timeout.command=timeout Defines how long Sendmail will wait when issuing a command.

Timeout.connect=timeout Defines how long Sendmail will wait for the connection.

Timeout.control=timeout Defines how long Sendmail will wait for control socket transmission to complete.

Timeout.datblock=timeout Defines how long Sendmail will wait for a block of data during the DATA phase.

Timeout.datafinal=timeout Defines how long Sendmail will wait for a response to the dot (.) terminates the DATA phase.

Timeout.datainit=timeout Defines how long Sendmail will wait for a response to a DATA command.

Timeout.fileopen=timeout Defines how long Sendmail will wait for a file to open.

Timeout.helo=timeout Defines how long Sendmail will wait for a response to HELO or EHLO command.

Timeout.hoststatus=timeout Defines how long Sendmail will hold host status information before deciding the information is stale.

Timeout.iconnect=timeout Defines how long Sendmail will wait for the connection to the first host in a message to complete.