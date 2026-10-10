# COMMANDS (CONT.)

| Use This Option | To Do This |
|---|---|
| **set keyword** | **retry = n** Retry *n* times if the server is not available. The default is four retries. |
| | **root = host** Set the name of the root server to *host*. The default is ns.internic.net. |
| | **timeout = n** Set the timeout to *n* seconds. The default is five seconds. |

# QUERY TYPES

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

# EXAMPLES

| This Command | Does the Following |
|---|---|
| rcp essay1.doc essay1.bak@lothlorien:/home/suzanne/Documents/Backup | Displays the numerical IP address for Yahoo. |
| rcp essay1.doc essay1.bak@lothlorien:/home/suzanne/Documents/Backup | Enters the interactive mode, in which you can use available commands. |