program interrupt key combination). Also, note that if the user is logged in multiple time you have to specify the tty device name to talk to a specific instances of the user login. You can run w or who command to find the tty names for each user login.

# telnet

Syntax: `telnet hostname_or_IP_address [port]`

This is the default Telnet client program. You can use this program to connect to a Telnet server. For example:

```
telnet shell.myportal.com
```

This command opens a Telnet connection to the shell.myportal.com system if the named host runs a Telnet server. Once a connection is opened, the command prompts you for a username and password and, on successful login, allows you to access a local user account on the Telnet server.

# wall

Syntax: `wall`

This command allows you to send a text message to everyone’s terminal as long as he or she has not disabled write access to the tty via the mesg n command. After you type wall, you can enter a single or multiline message and can send it by pressing Ctrl+D.

# Network Administrator’s Commands

The commands that I discuss in this section allow you to gather information on network services and on the network itself. Using these commands you can get a host name by IP, display or set host name of the system you are on, configure network interfaces, perform network queries, and so on.