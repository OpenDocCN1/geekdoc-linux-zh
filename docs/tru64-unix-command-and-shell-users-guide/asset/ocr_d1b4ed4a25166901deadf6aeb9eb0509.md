**Table 14–1: Options to the cu Command (cont.)**

| Option | Description |
|---|---|
| `-lline` | Specifies the name of a device (line) for the communication between two computers. The default is either a hardware asynchronous line, or a telephone line with an automatic dialer such as a modem. If your site has several communication lines, you may want to specify a particular line for your cu link. Usually, you do not have to specify a line or device; the default established during UUCP installation should be sufficient. If you want to connect to a remote computer but do not know its name, you can enter the cu command with the `-l` option and a variation of the standard device name tty (for example, `-ltty1`). Ask your system administrator for the device names at your site. |
| `-t` | Dials a terminal that has been set to *auto-answer*, and maps carriage return to carriage return/linefeed. |
| `host_name` | Specifies the name of the remote host with which you want to establish a connection. |
| `telno` | Specifies the telephone number in a remote connection using a modem. |

# 14.3.1.4 Local cu Commands

While connected by cu to a remote host, you can use local cu commands to perform the following tasks:

+   - Go back and forth between the local and remote hosts
+   - Change directories on the local host
+   - Copy files between local and remote hosts
+   - Terminate a remote connection

To return temporarily to the local host to work, type a tilde and an exclamation point (`~!`) at the remote system prompt; wait for the local system prompt to be displayed in the following form, where *local* is the name of the local host:

```
`~ [ local ] !`
```

Instead of waiting for the local system prompt to be displayed, you can enter the command immediately after typing the `~!` that accesses the local host. For example, while connected by cu to remote host moon, you can enter the following command to return to local host earth and use the cat command to read the `/usr/crew/r2/asimov/AI` file:

```
`moon^ ~!cat /usr/crew/r2/asimov/AI`
```