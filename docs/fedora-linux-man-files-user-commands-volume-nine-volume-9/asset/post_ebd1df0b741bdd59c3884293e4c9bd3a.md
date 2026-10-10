
# EXAMPLES

```
roqet sparql-query-file.rq
```

Run a SPARQL query contained in the local file sparql-query-file.rq. The data used would be described in FROM statements in the query file.

```
roqet -q -i sparql
```

Run a SPARQL query that is in the web at URI without an extra messages (quiet, -q).

```
roqet -q query-file.rq
```

Run an query (default language SPARQL) from a local file query-file.rq but using base URI to resolve any relative URIs.

```
roqet -q -i sparql -r x
```

Run a SPARQL query that is in the web at URI and format the results in the SPARQL Query Results XML format with no extra messages.

```
roqet -i sparql -e ‘SELECT * WHERE { ?s ?p ?o }’-D stuff.rdf
```

Run a SPARQL query given on the command line against data in the file stuff.rdf. The type of the file will be guessed and likely is of format RDF/XML.

```
roqet -t result.srx -r ht
```

Read a SPARQL query results in SPARQL Query Results XML format (default) and print it in HTML.

```
roqet -t result.ttl -R turtle -r csv
```

Read a SPARQL query results in RDF/Turtle format and print it in CSV.

## CONFORMING TO

*SPARQL 1.1 Query Language*, Steve Harris and Andy Seaborne (eds), W3C Recommendation, 21 March 2013

*SPARQL Query Results XML Format (Second Edition)*, Sandro Hawke (Second Edition ed), Jeen Broekstra and Dave Beckett (eds), W3C Recommendation, 21 March 2013.

## SEE ALSO

**(3),(3)**

## CHANGES

## AUTHOR

Dave Beckett -

# RPCCLIENT

## NAME

rpcclient - tool for executing client side MS-RPC functions

## SYNOPSIS

```
rpcclient [-Aauthfile] [-c<commandstring>] [-dddebuglevel] [-llogdir] [-N] [-s<sconconfigfile>] [-Uusername[%password]] [-Wworkgroup] [-IdestinationIP] {server}
```

## DESCRIPTION

This tool is part of the s suite.

rpcclient is a utility initially developed to test MS-RPC functionality in s itself. It has undergone several stages of development and stability. Many system administrators have now written scripts around it to manage Windows NT clients from their UNIX workstation.

## OPTIONS

- **server**

  NetBIOS name of Server to which to connect. The server can be any SMB/CIFS server. The name is resolved using the **name resolve order** [] line from s.

- **-c|—command=\<command string\>**

  Execute semicolon separated commands (listed below)

- **-I|—dest-ip IP-address**

  *IP address* is the address of the server to connect to. It should be specified in standard “a.b.c.d” notation.

  Normally the client would attempt to locate a named SMB/CIFS server by looking it up via the NetBIOS name resolution mechanism described above in the *name resolve order* parameter above. Using this parameter will force the client to assume that the server is on the machine with the specified IP address and the NetBIOS name component of the resource being connected to will be ignored.

  There is no default for this parameter. If not supplied, it will be determined automatically by the client as described above.

- **-p|—port port**

  This number is the TCP port number that will be used when making connections to the server. The standard (well-known) TCP port number for an SMB/CIFS server is 139, which is the default.

- **-d|—debuglevel=level**

  *level* is an integer from 0 to 10. The default value if this parameter is not specified is 0. The higher this value, the more detail will be logged to the log files about the activities of the server. At level 0, only critical errors and serious warnings will be logged. Level 1 is a reasonable level for day-to-day running - it generates a small amount of information about operations carried out.

  Levels above 1 will generate considerable amounts of log data, and should only be used when investigating a problem. Levels above 3 are designed for use only by developers and generate HUGE amounts of log data, most of which is extremely cryptic. Note that specifying this parameter here will override the **log level** [] parameter in the s.conf file.

- **-V|—version**

  Prints the program version number.

- **-s|---configfile=\<configuration file\>**

  The file specified contains the configuration details required by the server. The information in this file includes server-specific information such as what printcap file to use, as well as descriptions of all of the services that the server is to provide. See s.conf for more information. The default configuration file name is determined at compile time.

- **-l|---log-basename=logdirectory**

  Base directory name for log/debug files. The extension **.sclient** will be appended (e.g. log.sclient, log.smbd, etc…). The log file is never removed by the client.

- **---option=\<name\>=\<value\>**

  Set the s option“\<name\>” to value“\<value\>” from the command line. This overrides compiled-in defaults and options read from the configuration file.

- **-N|---no-pass**

  If specified, this parameter suppresses the normal password prompt from the client to the user. This is useful when accessing a service that does not require a password. Unless a password is specified on the command line or this parameter is specified, the client will request a password.

  If a password is specified on the command line and this option is also defined the password on the command line will be silently ignored and no password will be used.

- **-k|---kerberos**

  Try to authenticate with kerberos. Only useful in an Active Directory environment.

- **-C|---use-ccache**

  Try to use the credentials cached by winbind.

- **-A|---authentication-file=filename**

  This option allows you to specify a file from which to read the username and password used in the connection. The format of the file is
  username = <value> password = <value> domain = <value>

  Make certain that the permissions on the file restrict access from unwanted users.

- **-U|—user=username[%password]**

  Sets the SMB username or username and password.
  If %password is not specified, the user will be prompted. The client will first check the **USER** environment variable, then the **LOGNAME** variable and if either exists, the string is uppercased. If these environmental variables are not found, the username **GUEST** is used.

  A third option is to use a credentials file which contains the plaintext of the username and password. This option is mainly provided for scripts where the admin does not wish to pass the credentials on the command line or via environment variables. If this method is used, make certain that the permissions on the file restrict access from unwarranted users. See the -A for more details.

  Be cautious about including passwords in scripts. Also, on many systems the command line of a running process may be seen via the `ps` command. To be safe always allow rpcclient to prompt for a password and type it in directly.

- **-S|—signing on|off|required**

  Set the client signing state.

- **-P|—machine-pass**

  Use stored machine account password.

- **-e|—encrypt**

  This command line parameter requires the remote server support the UNIX extensions or that the SMB3 protocol has been selected. Requests that the connection be encrypted. Negotiates SMB encryption using either SMB3 or POSIX extensions via GSSAPI. Uses the given credentials for the encryption negotiation (either kerberos or NTLMv1/v2 if given domain/username/password triple. Fails the connection if encryption cannot be negotiated.

- **—pw-nt-hash**

  The supplied password is the NT hash.

- **-n|—netbiosname <primary NetBIOS name>**

  This option allows you to override the NetBIOS name that s uses for itself. This is identical to setting the **netbios name** [] parameter in the s.conf file. However, a command line setting will take precedence over settings in s.conf.

- **-i|—scope <scope>**

  This specifies a NetBIOS scope that nlookup will use to communicate with when generating NetBIOS names. For details on the use of NetBIOS scopes, see rfc1001.txt and rfc1002.txt. NetBIOS scopes are very rarely used, only set this parameter if you are the system administrator in charge of all the NetBIOS systems you communicate with.

- **-W|—workgroup=domain**

  Set the SMB domain of the username. This overrides the default domain which is the domain defined in s.conf. If the domain specified is the same as the servers NetBIOS name, it causes the client to log on using the servers local SAM (as opposed to the Domain SAM).

- **-O|—socket-options socket options**

  TCP socket options to set on the client socket. See the socket options parameter in the s.conf manual page for the list of valid options.

- **-?|—help**

  Print a summary of command line options.

- **—usage**

  Display brief usage message.
