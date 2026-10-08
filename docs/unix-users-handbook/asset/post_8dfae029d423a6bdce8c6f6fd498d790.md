
that invoked rlogin. The rlogin job can be resumed with the fg command (see csh(1), ksh(1), and sh-posix(1)). e^Y suspends only the input process; output from the remote login continues to be displayed.

If you "daisy-chain" remote logins (for example, you rlogin from host A to host B and then rlogin from host B to host C) without setting unique escape characters, you can repeat the escape character until it reaches your chosen destination. For example, the first escape character, e, is seen as an escape character on host A; the second e is passed as a normal character by host A and seen as an escape character on host B; a third e is passed as a normal character by hosts A and B and accepted as a normal character by host C.

### Remote Host Name As Command

The system administrator can arrange for more convenient access to a remote host (rhost) by linking remsh to /usr/hosts/rhost, allowing use of the remote host name (rhost) as a command (see remsh(1)). For example, if remotehost is the name of a remote host and /usr/hosts/remotehost is linked to remsh, and if /usr/hosts is in your search path, the command:

```
remotehost
```

is equivalent to:

```
rlogin remotehost
```

### RETURN VALUES

rlogin sends an error message to standard error and returns a nonzero value if an error occurs before the connection to the remote host is completed. Otherwise, it returns a zero.

### DIAGNOSTICS

Diagnostics can occur from both the local and remote hosts. Those that occur on the local host before the connection is completely established are written to standard error. Once the connection is established, any error messages from the remote host are written to standard output, like any other data.

- login/tcp: Unknown service
  - rlogin was unable to find the login service listed in the /etc/services database file.

- There is no entry for you (user ID username) in /etc/passwd
  - rlogin was unable to find your user ID in the password file.
  - Next Step: Contact your system administrator.

- system call:...
  - An error occurred when rlogin attempted the indicated system call. See the appropriate manual entry for information about the error.

### EXAMPLES

Log in as the same user on the remote host remote:

```
rlogin remote
```

Set the escape character to a !, use a seven-bit data connection, and attempt a login as user guest on host remhost:

```
rlogin remhost -e! -7 -l guest
```

Assuming that your system administrator has set up the links in /usr/hosts, the following is equivalent to the previous command:

```
rhost -e! -7 -l guest
```

### WARNINGS

For security purposes, the /etc/hosts.equiv and .rhosts files should exist, even if they are empty. These files should be readable and writable only by the owner. See host.equiv(4) for more information.

Note also that all information, including any passwords asked for, is passed unencrypted between the two hosts.

rlogin is unable to transmit the Break key as an interrupt signal to the remote system, regardless of whether the user has set stty brkint on the local system. The key assigned to SIGINT with the command stty intr c should be used instead (see stty(1)).

### AUTHOR

rlogin was developed by the University of California, Berkeley.

### FILES

| File | Description |
| :--- | :--- |
| $HOME/.rhosts | User's private equivalence list |
| /etc/hosts.equiv | List of equivalent hosts |
| /usr/hosts/* | For rhost version of the command |

### SEE ALSO

csh(1), ksh(1), login(1), remsh(1), sh(1), sh-bourne(1), sh-posix(1), stty(1), telnet(1), rlogind(1M), hosts(4), hosts.equiv(4), inetd.conf(4), services(4), termio(7), tty(7).

---

### NAME

rlogin - remote login

### SYNOPSIS

```
rlogin rhost [-7] [-8] [-ee] [-f/F] [-k realm] [-l username] [-P]
rhost  [-7] [-8] [-ee] [-f/F] [-k realm] [-l username]  [-P]
```

### DESCRIPTION

The rlogin command connects your terminal on the local host to the remote host (rhost). rlogin acts as a virtual terminal to the remote system. The host name rhost can either be the official name or an alias as listed in the file /etc/hosts (see hosts(4)).

The terminal type specified by the current TERM environment variable is propagated across the network and used to set the initial value of your TERM environment variable on the remote host. Your terminal baud rate is also propagated to the remote host, and is required by some systems to set up the pseudo-terminal used by rlogind (see rlogind(1M)).

All echoing takes place at the remote site, so that (except for delays) the remote login is transparent.

If at any time rlogin is unable to read from or write to the socket connection on the remote host, the message Connection closed is printed on standard error and rlogin exits.

In a Kerberos V5 Network Authentication environment, rlogin uses the Kerberos V5 protocol to authenticate the connection to a remote host. If the authentication is successful, user authorization will be performed according to the command line options selected for rlogin (i.e., `-K`, `-R`, `-r`, or `-k`). A password will not be required, so a password prompt will not be seen and a password will not be sent over the network where it can be observed. For further information on Kerberos authentication and authorization see the Secure Internet Services man page, `sis(5)` and `rlogind(1M)`.

Although Kerberos authentication and authorization may apply, the Kerberos mechanism is not applied to the login session. All information transferred between your host and the remote host is sent in cleartext over the network.

### Options

`login` recognizes the following options. Note that the options follow the `rhost` argument.

- `-7`
  Set the character size to seven bits. The eighth bit of each byte sent is set to zero (space parity).

- `-8`
  Use an eight-bit data path. This is the default HP-UX behavior.

  To use eight-bit characters, the terminal must be configured to generate either eight-bit characters with no parity, or seven bit characters with space parity. The HP-UX implementation of `rlogind` (see `rlogind(1M)`) interprets seven bit characters with even, odd, or mark parity as eight-bit non-USASCII characters. You may also need to reconfigure the remote host appropriately (see `sty(1)` and `tty(7)`). Some remote hosts may not provide the necessary support for eight-bit characters. In this case, or if it is not possible to disable parity generation by the local terminal, use the `-7` option.

- `--ee`
  Set the escape character to e. There is no space separating the option letter and the argument character. To start a line with the escape character, two of the escape characters must be entered. The default escape character is tilde (`~`). Some characters may conflict with your terminal configuration, such as `^S`, `^Q`, or backspace. Using one of these as the escape character may not be possible or may cause problems communicating with the remote host (see `sty(1)` and `tty(7)`).

- `-f`
  Forward the ticket granting ticket (TGT) to the remote system. The TGT is not forwardable from there.

- `-F`
  Forward the TGT to the remote system and have it forwardable from there to another remote system. `-f` and `-F` are mutually exclusive.

- `-k realm`
  Obtain tickets from the remote host in the specified realm instead of the remote host's default realm as specified in the configuration file `krb.realms`.

- `-l username`
  Set the user login name on the remote host to `username`. The default name is the current account name of the user invoking `login`.

- `-P`
  Disable Kerberos authentication. Only applicable in a secure environment based on Kerberos V5. When this option is specified, a password is required and the password is sent across the network in cleartext. To bypass the normal login/password sequence, you can login to a remote host using an equivalent account in a manner similar to remsh. See hosts.equiv(4) for details.

rlogin can be controlled with two-character escape sequences, in the form ex, where e is the escape character and x is a code character described below. Escape sequences are recognized only at the beginning of a line of input. The default escape character is tilde (~). It can be changed with the -e option.

The following escape sequences are recognized:

- `ey`
  If y is NOT a code character described below, pass the escape character and y as characters to the remote host.

- `ee`
  Pass the escape character as a character to the remote host.

- `e.`
  Disconnect from the remote host.

- `e!`
  Escape to a subshell on the local host. Use exit to return to the remote host.

If rlogin is run from a shell that supports job control (see csh(1), ksh(1), and sh-posix(1)), escape sequences can be used to suspend rlogin. The following escape sequences assume that ^Z and ^Y are set as the user's susp and dsusp characters, respectively (see stty(1) and termio(7)).

- `e^Z`
  Suspend the rlogin session and return the user to the shell that invoked login. The rlogin job can be resumed with the fg command (see csh(1), ksh(1), and sh-posix(1)). e^Z suspends both rlogin processes: the one transmitting user input to the remote login, and the one displaying output from the remote login.

- `e^Y`
  Suspend the rlogin session and return the user to the shell that invoked login. The rlogin job can be resumed with the fg command (see csh(1), ksh(1), and sh-posix(1)). e^Y suspends only the input process; output from the remote login continues to be displayed.

If you "daisy-chain" remote logins (for example, you rlogin from host A to host B and then rlogin from host B to host C) without setting unique escape characters, you can repeat the escape character until it reaches your chosen destination. For example, the first escape character, e, is seen as an escape character on host A; the second e is passed as a normal character by host A and seen as an escape character on host B; a third e is passed as a normal character by hosts A and B and accepted as a normal character by host C.

### Remote Host Name As Command

The system administrator can arrange for more convenient access to a remote host (rhost) by linking remsh to /usr/hosts/rhost, allowing use of the remote host name (rhost) as a command (see remsh(1)). For example, if remotehost is the name of a remote host and /usr/hosts/remotehost is linked to remsh, and if /usr/hosts is in your search path, the command:

```
remotehost
```
