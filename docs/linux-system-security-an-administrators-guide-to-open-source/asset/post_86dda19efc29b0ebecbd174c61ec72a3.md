
Table 11.7 Keywords in $HOME/.ssh/config or /etc/ssh/ssh_config

| Flag | Description |
| --- | --- |
| -C | Compresses all data using gzip. For performance purposes, useful only over slow connections such as modem lines. Does not enhance security. The level of compression may be controlled by the compressionLevel option (see Table 11.7). |
| -L port:host:hostport | Specifies that port is to be forwarded to hostport on the remote host. Only root can forward privileged ports. Details are given in Local Forwarding on page 308. |
| -R port:host:hostport | Specifies that the remote port is to be forwarded to hostport on the host. Only after attaining root privilege on the remote system can privileged ports be forwarded. A further description is provided in Remote Forwarding on page 310. |

Table 11.7 Keywords in $HOME/.ssh/config or /etc/ssh/ssh_config

| Keyword | Description |
| --- | --- |
| Host | Takes a hostname or IP address as a value. The wildcards * or ? may be used. This keyword causes all subsequent keywords, up to the next Host keyword, to apply only to the indicated host. In this way, one configuration file may be used to apply to many hosts. The entry Host * causes the settings to apply to all hosts. The hostname to match this keyword is the hostname given on the command line, as in ssh hostname. |
| BatchMode | If yes, password prompting will be disabled. Useful for scripting, but requires that an agent (see Managing RSA Authentication with ssh-agent and ssh-add on page 301) be running or passwords must be provided in the script. The default is no. |
| Cipher | Specifies the symmetric cipher. Available options are idea, des, 3des, blowfish, arcfour, and none. The default for the U.S. version is blowfish; otherwise it is idea. The none option turns off encryption, and all data transfers via ssh will be in the clear. The none option is for debugging only. This setting may be overridden by the -c command line option to ssh; see Table 11.6 on page 276. |
| ClearAllForwardings | If yes, causes all forwarding in the configuration file and at the command line to be cleared. The default is no; however, scp will set this option to yes to avoid failures. |
| Compression | If yes, gzip compression will be used. The default is no. This setting may be overridden by the -C command line option to ssh; see Table 11.6 on page 276. |
| CompressionLevel | Specifies the gzip compression level (see the gzip(1) man page). Acceptable values are integers between 1 and 9, inclusive—1 indicates fast but reduced compression; 9 is slow but optimal compression. The default is 6. |
| ConnectionAttempts | Specifies the number of tries per second before trying *rsh* or (if *rsh* is disabled) failing. The default is 1. Increasing this value may be useful for scripting. |
| EscapeChar | Sets the escape character for sessions with a pseudoterminal (pty). It is `~` by default. Setting the value to *none* disables escapes. This setting may be overridden by the *-e* command line option to *ssh*; see Table 11.6 on page 276. |
| FallBackToRsh | If *yes* (the default), whenever the connection with *sshd* on the server fails, *in.rshd* is tried. In such a case, a warning message regarding the failure is displayed to the client. |
| ForwardAgent | Specifies whether or not the connection to *ssh-agent* will be forwarded to the remote server. The default is *yes*. This is further described in Disabling *X* and Agent Forwarding on page 303. |
| ForwardX11 | Specifies whether *X* Window Systems will automatically be redirected through the *SSH*-encrypted tunnel and automatically set the *DISPLAY* environment variable. The default is *yes*. Further details regarding this option are provided in Managing *RSA* Authentication with *ssh-agent* and *ssh-add* on page 301. |
| GatewayPorts | If *yes* (the default), then remote hosts may connect to locally forwarded ports. |
| GlobalKnownHostsFile | Defaults to */etc/ssh_known_hosts*, but to */etc/ssh/ssh_known_hosts* in the *RPMs*. Requires an absolutely qualified path to filename. |
| HostName | Takes a hostname or IP address as its value. Sets the host to login to. This option is not set by default, and the destination host (server) must be specified on the command line. |
| IdentityFile | Specifies the file containing the Private User Key. The default is $HOME/.ssh/identity. |
| KeepAlive | If *yes* (the default), *ssh* will check connectivity to the server periodically. If connectivity cannot be verified, *ssh* closes the connection. This is true even if the verification fails due to a temporary routing problem. To disable this mechanism, you must set this keyword to *no* in both */etc/ssh/sshd_config* and */etc/ssh/ssh_config* or $HOME/.ssh/config. |
| LocalForward | Requires a value of the form *port host:hostport*. Specifies that *port* is to be forwarded to *hostport* on the remote host. Only *root* can forward privileged ports. Details are given in *Local Forwarding* on page 308. This entry may be overridden by the *-L* command line option to *ssh*; see Table 11.6 on page 276. |
| NumberOfPasswordPrompts | Specifies the number of password prompts before giving up. The default is 1. The server sets a hard limit of 5 attempts, so setting this value greater than 5 will have the effect of setting it to 5. |
| **PasswordAuthentication** | If **yes** (the default), **ssh** will attempt password authentication when necessary. |
| **PasswordPromptHost** | If **yes** (the default), the remote hostname will be included in the password prompt. |
| **PasswordPromptLogin** | If **yes** (the default), the remote username will be included in the password prompt. |
| **Port** | Specifies the destination port number to connect to on the server. The default is **22**. |
| **ProxyCommand** | Specifies the command to use to connect to the server instead of **ssh**. The command string extends to the end of the line and is invoked by **/bin/sh**. Note that **%p** expands to the port number and **%h** expands to the remote host. |
| **RemoteForward** | Requires a value of the form **port:host:hostport**. Specifies that the remote port is to be forwarded to **host:port** on the host. Only after attaining root privilege on the remote system can privileged ports be forwarded. A further description is provided in *Remote Forwarding* on page **310**. This entry may be overridden by the **-R** command line option to **ssh**; see Table **11.6** on page **276**. |
| **RhostsAuthentication** | If **yes**, Rhosts Authentication is attempted. The default is **no**. |
| **RhostsRSAAuthentication** | In order to enable this scheme, this keyword must be set to **yes** here and in the **/etc/ssh/ssh_config** on the server. See *Rhosts and RSA Authentication* on page **260** for a detailed discussion of this scheme. |
| **RSAAuthentication** | If **yes** (the default), then Rhosts and RSA Authentication is attempted. In order to enable this scheme, this keyword must be set to **yes** here and in **/etc/ssh/ssh_config** on the server. See *Rhosts and RSA Authentication* on page **260** for a detailed discussion of this scheme. |
| **RSAAuthentication** | If **yes** (the default), then RSA Authentication is attempted. In order to enable this scheme, this keyword must be set to **yes** here and in **/etc/ssh/ssh_config** on the server. See *RSA Authentication* on page **261** for a detailed discussion of this scheme. |
| **StrictHostKeyChecking** | This option takes one of three arguments—**yes**, **no**, or **ask**. If **yes**, then the client will never accept unverifiable Public Host Keys from the server (verifiable keys are found in either **$HOME/.ssh/known_hosts** or **/etc/ssh/ssh_known_hosts** on the client). If **no**, then the client will always add unverifiable server Host Keys into the file **$HOME/.ssh/known_hosts**. If **ask** (the default), then the client will always prompt the user as to whether or not the unverifiable server Public Host Key should be added to the file **$HOME/.ssh/known_hosts**. |
