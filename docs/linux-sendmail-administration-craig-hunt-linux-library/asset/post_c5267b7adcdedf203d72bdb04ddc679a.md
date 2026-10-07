
ControlSocketName=path Defines the path of the Unix control socket used to manage daemon connections. By default, this is not defined.

DaemonPortOptions=options Sets SMTP server options. The options keyword=value pairs. The options are:

- Name=type, where type is the type of daemon. type can be either MTA or MSA.
- Port=portnumber, where portnumber is any valid port number. It is specified with the port or the name found in /etc/services. The default is port 25 for the MTA and 587 for the MSA.
- Addr=mask, where mask is an IP address mask specified either in dotted decimal notation or as a network name. The default is INADDR_ANY, which accepts all addresses.
- Family=addressfamily, where addressfamily is a valid address family. The default is IN, which allows IP addresses to be used.
- Listen=n, where n is the number of queued connections allowed. The default is 10.
- SndBufSize=n, where n is the send buffer size.
- RcvBufSize=n, where n is the receiver buffer size.
- DataFileBufferSize=bytes Defines the maximum amount of memory that can be used to buffer a data file.
- DeadLetterFile=file Defines the file where messages that cannot be returned to the sender or to the postmaster account are stored.
- DefaultAuthInfo=file Defines the file that contains the authentication information needed for outbound connections.
- Charset=charset Defines the character set placed in the MIME Content-Type header where eight-bit data is converted to seven-bit format. The default is unknown-utf8. This option is overridden by the Charset field of the mail descriptor.
- DefaultUser=user[:group] Sets the user ID and group ID for mailers without the S flag in their defaults. If group is omitted, the group associated with the user in /etc/passwd file is used. The default is 1:1.
- DeliveryMode=mode Starts Sendmail in the specified delivery mode. The mode can be interactive, background, queue, or deferred. The default is background. Sendmail can change the mode during a run.
- DHParameters=parameters Defines the DH parameters used when Sendmail DSA/DH encryption.

DialDelay=delay delaytime is the number of seconds Sendmail should delay before redial a failed connection on dial-on-demand networks. The default is 0 (no redial).

DontBlameSendmail=options Disables Sendmail's security checks. Disabling security is generally a bad idea, so this option should be used only if absolutely necessary. options is a comma-separated list of keywords that disable specific security checks. Table C.4 lists the keywords and the effect each one has on security.

## Table C.4 Possible Settings for the DontBlameSendmail Option

| Keyword | What It Tells Sendmail |
| --- | --- |
| AssumeSafeChown | The chosen command is safe because it is only available to the root user. |
| ClassFileInsafeDirPath | Accept any directory path in an F command. |
| DontWarnForwardFileInsafeDirPath | Don't issue warning about the path of the . forward file. |
| ErrorHeaderInsafeDirPath | Accept the error header file less of its directory path. |
| FileDeliveryToHardLink | Permit delivery to a file that is really a hard link. |
| FileDeliveryToSymLink | Permit delivery to a file that is really a symbolic link. |
| ForwardFileInsafeDirPath | Accept a . forward file even if it is in an unsafe directory. |
| ForwardFileInsafeDirPathSafe | Accept program and file references from a . forward file even if it is in an unsafe directory. |
| ForwardIngroupWritableDirPath | Accept a . forward file even if it is in a group-writeable directory. |

## Appendix C Sendmail Variables, Options, and Flags

**Table C.4** Possible Settings for the DontBlameSendmail Option (continued)

| Keyword | What It Tells Sendmail |
| --- | --- |
| GroupWritableAliasFile | Accept the aliases file even if it is group-writable. |
| GroupWritableDirPathSafe | Accept all group-writable directories as "safe.". |
| GroupWritableForwardFileSafe | Accept a .forward file if it is group-writable. |
| GroupWritableIncludeFileSafe | Accept :include: files if they are group-writable. |
| HelpFileInUnsafeDirPath | Accept the help file even if it is in an unsafe directory. |
| IncludeFileInUnsafeDirPath | Accept :include: files if they are from unsafe directories. |
| IncludeFileInUnsafeDirPath | Accept program and file references from an :include: file even if it is in an unsafe directory. |
| IncludeFileIngroupWritableDirPath | Accept :include: file even if it is in a group-writable directory. |
| InsufficientEntropy | Use STARTTLS even if the random seed generator for SSL is inadequate. |
| LinkedAliasFileInWritableDir | Accept an aliases file that is a link in a writable directory. |
| LinkedClassFileInWritableDir | Load class values from files that are links in writable directories. |
| LinkedForwardFileInWritableDir | Accept .forward files that are links in writable directories. |

## Table C.4 Possible Settings for the DontBlameSendmail Option (continued)

| Keyword | What It Tells Sendmail |
|---|---|
| LinkedIncludeFileInWritableDir | Accept: include files that are in writeable directories. |
| LinkedMapInWritableDir | Accept database files that are in writeable directories. |
| LinkedServiceSwitchInWritableDir | Accept a service switch file that is a link in a writeable directory. |
| MapInsafeDirPath | Accept database files that are in unsafe directories. |
| NonRootSafeAddr | Don't flag file and program as unsafe when Sendmail is not running as root. |
| RunProgramInsafeDirPath | Run programs that are in writeable directories. |
| RunWritableProgram | Run programs that are group and world wide. |
| Safe | Leave all of the safety checks on. This is the default. |
| TrustStickyBit | Trust group and world wide if the sticky bit is set. |
| WorldWritableAlias | Accept the aliases file even if it is world wide. |
| WriteMapToHardLink | Write to databases files even if they are hard links. |
| WriteMapToSymLink | Write to a symbolic link. |

## Appendix Sendmail Variables, Options, and Flags

## Table C.4 Possible Settings for the DontBlSendmail Option (continued)

| Keyword | What It Tells Sendmail |
|---|---|
| WriteStatsToHardLink | Write to the status file if it is really a hard link. |
| WriteStatsToSym | Write to the status file if it is symbolic link. |

DontExpandCnames Disables the conversion of nicknames to canonical names.
DontInitGroups Limits the mail delivery agent route for a user to the group associated with that user using the /etc/passwd file. It is used to reduce the load on NIS servers.
DontProbeInterfaces If true, stops Sendmail from adding the names and addresses of the network interfaces to w. The default is false, so interface and addresses are stored in w.

DontPruneRoutes Prevents Sendmail from optimizing explicit mail routes. Normally, Sendmail makes a route as direct as possible. However, optimizing the route may not be appropriate for systems located behind a firewall.

DoubleBounce=address Tells Sendmail where to send the report of an error that occurs when sending an error message. The default for address is postmaster.

EightBitMode=action Specifies how undeclared eight-bit data is handled. The possible actions are: s–strict, reject undeclared eight-bit data; m–mime, convert the data to MIME format; and p—send the data through unaltered.

ErrorHeader=file-or-message Specifies the file or message that is prepended to outgoing error messages. If file-or-message is the path to a file, it must begin with a slash. If this option is not defined, nothing is prepended to error messages.

ErrorMode=action tells Sendmail how to handle error messages. If this option is not defined, error messages are printed. The valid actions are:

- * Print error messages.
- Return an error status but send no error message.
- Mail the error message back to the sender.
- Write the error messages to the user’s terminal.
- Mail the error message back, but always give zero exit status.
