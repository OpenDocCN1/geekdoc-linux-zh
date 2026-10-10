# **OPTIONS**


| Use This Option | To Do This |
|---|---|
| -a, --all | Get all messages from the server. |
| -b n, --batchlimit n | Retrieve a maximum of n messages. |
| -B n, --fetchlimit n | Retrieve a maximum of n messages in a single poll. |
| --bsmtp filename | Append fetched mail to a BSMTP file. |
| -F, --flush | Delete read messages from the POP3 or IMAP server. |
| -k, --keep | Keep retrieved messages on the server instead of deleting them, which is the default behavior. |
| -l n, --limit n | Specify the maximum size (in bytes) for messages to be downloaded. Messages larger than this size are skipped. |
| -p protocol, --protocol protocol | Use the specified protocol when connecting to the mail server. If you do not specify a protocol, fetchmail attempts to detect the protocol automatically. |
| -s, --silent | Hide program messages. |
| --ssl | Use encryption if the server supports it. |
| -t n, --timeout n | Set the server non-response time to n seconds. |
| -u username, --username username | Log on with the specified username. |
| -v, --verbose | Show all messages. |


# **fetchmailconf**

fetchmailconf
Launches an interactive editor that creates the configuration file (`/.fetchmailrc`) for the `fetchmail` utility. If `fetchmailconf` is not available on your system, you can download a copy from Internet distribution sites such as `http://www.freshmeat.net`.