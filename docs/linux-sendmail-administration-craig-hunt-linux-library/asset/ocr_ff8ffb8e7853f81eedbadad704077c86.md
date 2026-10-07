ControlSocketName=path Defines the path of the Unix control socket used to manage daemon connections. By default, this is not defined.

DaemonPortOptions=options Sets SMTP server options. The options keyword=value pairs. The options are:

Name=type, where type is the type of daemon. type can be either MTA or MSA.
Port=portnumber, where portnumber is any valid port number. It is specified with the port or the name found in /etc/services. The default is port 25 for the MTA and 587 for the MSA.

Addr=mask, where mask is an IP address mask specified either in dotted decimal notation or as a network name. The default is INADDR_ANY, which accepts all addresses.

Family=addressfamily, where addressfamily is a valid address family. The default is IN, which allows IP addresses to be used.

Listen=n, where n is the number of queued connections allowed. The default is 10.

SndBufSize=n, where n is the send buffer size.

RcvBufSize=n, where n is the receiver buffer size.

DataFileBufferSize=bytes Defines the maximum amount of memory that can be used to buffer a data file.

DeadLetterFile=file Defines the file where messages that cannot be returned to the sender or to the postmaster account are stored.

DefaultAuthInfo=file Defines the file that contains the authentication information needed for outbound connections.

Charset=charset Defines the character set placed in the MIME Content-Type header where eight-bit data is converted to seven-bit format. The default is unknown-utf8. This option is overridden by the Charset field of the mail descriptor.

DefaultUser=user[:group] Sets the user ID and group ID for mailers without the S flag in their defaults. If group is omitted, the group associated with the user in /etc/passwd file is used. The default is 1:1.

DeliveryMode=mode Starts Sendmail in the specified delivery mode. The mode can be interactive, background, queue, or deferred. The default is background. Sendmail can change the mode during a run.

DHParameters=parameters Defines the DH parameters used when Sendmail DSA/DH encryption.