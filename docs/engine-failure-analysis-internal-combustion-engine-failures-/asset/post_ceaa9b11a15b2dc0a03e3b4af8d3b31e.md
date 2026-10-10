
## COMMANDS

| Use This Option | To Do This |
| :--- | :--- |
| `host [server]` | Look up information for the specified host. Optionally, obtain this information from the specified server. |
| `lserver server` | Change the default server. |
| `root` | Change the default server for the root of the domain name space. The default is ns.internic.com. |
| `ls [option]` | List available host names and IP addresses for the specified domain. Optionally, append the output to the specified filename. You can use the following options: |
| `-t querytype` | List all the records of the specified query type. (See the table Query Types later in this section.) |
| `-a` | List aliases of hosts in the domain. |
| `-d` | List all records for the domain. |
| `-h` | List the CPU and operating system type for the domain. |
| `help, ?` | Show available commands. |
| `exit` | Quit nslookup. |
| `set keyword` | Change the lookup method. Available `keyword = value` options are as follows: |
| `all` | Show the current values of set options. |
| `class = value` | Change the query class to IN (Inter-net classes), CHAOS (Chaos classes), HESIOD (MIT Athena class), or ANY (any of the options). |
| `domain = name` | Change to the specified default domain. The default is to use the current host’s domain. |
| `srchlist = list` | Use the comma-separated list of domains to search. |
| `port = n` | Change the default DNS port to *n*. The default is port 53. |
| `querytype = query type` | Use one of the query types listed in the Query Types table later in this section. The default is type A (Internet address). |
| `recurse` | Query other servers if the default server does not have the information. This is the default setting. Use `no recurse` to turn this feature off. |
| **set keyword** | **retry = n** Retry *n* times if the server is not available. The default is four retries. |
| | **root = host** Set the name of the root server to *host*. The default is ns.internic.net. |
| | **timeout = n** Set the timeout to *n* seconds. The default is five seconds. |

## QUERY TYPES

| Use This Query Type | To View the Following Information |
|---|---|
| A | The host's Internet address |
| CNAME | The canonical name for an alias |
| HINFO | The host CPU and operating system type |
| MINFO | The mailbox or mail list information |
| MX | The mail exchanger |
| NS | The name server for the named zone |
| PTR | The host name if the query is an Internet address, otherwise, the pointer to other information |
| SOA | The domain's "start-of-authority" information |
| TXT | The text information |
| UINFO | The user information |
| WKS | The supported well-known services |

## EXAMPLES

| This Command | Does the Following |
|---|---|
| `nslookup www.yahoo.com` | Displays the numerical IP address for Yahoo. |
| `nslookup` | Enters the interactive mode, in which you can use available commands. |

## ping

**ping** [ option ] host

Sends packets of Internet data to the specified host to see whether the host is online and capable of exchanging data. **ping** is frequently used to verify that a system is indeed connected to the Internet and capable of exchanging data with other Internet hosts.

*See also netstat, nslookup.*

### OPTIONS

| Use This Option | To Do This |
|-----------------|------------|
| -c n | Stop after receiving n packets. |
| -i n | Wait n seconds between sending each packet. The default is one second. |
| -f | Sends as many packets as possible. Requires root or superuser status. |
| -n | Show the numeric IP addresses only. |
| -P pattern | Pad the output with a specified pattern of up to 16 bytes. |
| -q | Hide messages. |
| -r | Ping the host directly without using routing tables. |
| -R | Record the route. |
| -s n | Send n bytes of data in each packet. The default is 56, which translates into 64 bytes when the header data is added. |
| -v | Show all messages. |

### EXAMPLES

| This Command | Does the Following |
|--------------|--------------------|
| ping 207.46.131.30 | Pings the specified IP address. |
| ping www.yahoo.com | Pings the specified domain. |

## rcp

`rcp` [ option ] source file destination file

Copies the specified source file to the destination file. The source file or the destination file can be located on the local, or a remote, machine and can refer to a file or a directory. To indicate a local file, type the filename. You can also specify the path name if the file is not located in the working directory. To indicate a remote file, type the filename followed by @, the name of the host, and the path name on the host (see the Examples later in this section).

### OPTIONS

| Use This Option | To Do This |
|---|---|
| `-p` | Preserve the original modification times and permission modes of the source files if possible |
| `-r` | Copy the specified directory and all associated subdirectories (recursive mode) |

### EXAMPLES

| This Command | Does the Following |
|---|---|
| `rcp essay1.doc essay1.bak@lothlorien:/home/suzanne/Documents/Backup` | Copies the specified file (`essay1.doc`) to the remote machine (`lothlorien`) and writes it to the file named `/home/suzanne/Documents/Backup/essay1.bak`. |
| `rcp -r Poems Poems@lothlorien:/home/suzanne/Documents` | Copies the specified directory (`Poems`) and all associated subdirectories to the remote machine (`lothlorien`). Creates a new directory called `Poems`, if necessary, within the `/home/suzanne/Documents` directory. |

## rpcinfo

```
rpcinfo [ option ] [ host ]
```

Displays information about the Network File System. This utility provides a useful way to check that all the required NFS daemons are installed and running properly.

### OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -n n | Display information about the port number specified by n |
| -u host n | Display information about the program number n running on the specified host |
| -P [ host ] | Display information about the NFS daemons running on the current system or the specified host |

### EXAMPLE

| This Command | Does the Following |
| --- | --- |
| rpcinfo -p | Displays a list of all the NFS daemons currently running, if any. |

## showmount

```
showmount [ option ] [ host ]
```

Displays the Network File System mounts available. Optionally, shows the mounts available on the specified host.

### OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -a, -all | List both the client hostname and mounted directory in host:dir format |
| -d, --directories | List only mounted directories |
| -e, --exports | Show the NFS server's export list |
| -h, --help | Show available options |
| -v, --version | Display the version number |

### EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| showmount -a | Displays all available NFS mounts. |
| showmount lothlorien | Displays the mounts available from the specified server (lothlorien). |
| showmount -e | Displays the exports made available from this system's NFS server. |

## smbclient

**smbclient** *service* [ *option* ]

Launches an interactive Samba utility that closely resembles *ftp*. With this utility, you can transfer files and perform other file-related operations on remote Samba directories. See the Commands table for the commands you can use in the utility's interactive mode.

*See also* **smbmount**.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -B *size* | Change the transmit/send buffer to the specified size in bytes. |
| -h | Show the available options. |
| -I *address* | Connect to the specified IP address. |
| -L | View options available on the server. |
| -l *filename* | Log operational data to the specified filename. |
| -N | Suppress the password prompt for services that do not require a password. |
| -n *name* | Use the specified name instead of the local machine's hostname. |
| -p *port* | Use the specified port to connect to the server. The default is 139. |
| -s *filename* | Use the specified filename as the Samba configuration file. |
| -T *option* | Create a *tar* backup. Available options are as follows: |
| -U *username* | Use the specified username. |
| -W WORKGROUP | Use the specified WORKGROUP (typed in capital letters) instead of the default workgroup defined in *smb.conf*. |

### COMMANDS

| Use This Command | To Do This |
| ? [ *command* ] | Show help options or show help for the specified command. |
