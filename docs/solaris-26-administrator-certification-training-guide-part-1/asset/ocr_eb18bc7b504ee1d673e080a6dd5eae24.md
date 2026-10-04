The -i option specifies the inactive (disabled) response message sent to a terminal or modem when a user attempts to log in to a disabled port.

To keep the modem connection when a user logs off from a host, type

```
ttyadm -h
```

The system will not hang up on a modem before setting or resetting to the default or specified value. If ttyadm -h is not used, the host will hang up the modem when the user logs out of a host.

Use the -r option with ttyadm to require the user to type a character before the system displays a prompt:

```
ttyadm -r
```

The -r option specifies that ttymon should require the user to type a character or press Return a specified number of times before the login prompt appears. This option prevents a terminal server from issuing a welcome message that the Solaris host might misinterpret as a user trying to log in. Without the -r option, the host and terminal server might begin looping and printing prompts to each other.

Options to the ttyadm command are described in Table 12-8.

# Table 12-8 ttyadm Command Options

| Command Option | Description |
|---|---|
| -b | The bidirectional port flag. When this flag is set, the line can be used in both directions. |
| -h | Sets the hangup flag for the port. |
| -i | Specifies the inactive (disabled) response message. |
| -l | Specifies which TTY label in /etc/ttydefs to use. |
| -m | Specifies the streams modules to push before invoking this service. |
| -p | Specifies the prompt message, for example, login:. |
| -d | Specifies the full pathname to the device to use for the TTY port. |
| -r count | When the -r option is invoked, ttymon waits until it receives data from the port before it displays a prompt. |
| -s | Specifies the full pathname of the service to invoke when a connection request is received. If arguments are required, enclose the command and its arguments in quotation marks (""). |
| -T | Sets the terminal type. |