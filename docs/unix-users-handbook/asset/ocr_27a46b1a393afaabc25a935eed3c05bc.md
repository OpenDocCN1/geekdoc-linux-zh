To use eight-bit characters, the terminal must be configured to generate either eight-bit characters with no parity, or seven bit characters with space parity. The HP-UX implementation of rlogin(1M)) interprets seven bit characters with even, odd, or mark parity as eight-bit non-USASCII characters. You may also need to reconfigure the remote host appropriately (see stty(1) and tty(7)). Some remote hosts may not provide the necessary support for eight-bit characters. In this case, or if it is not possible to disable parity generation by the local terminal, use the `-7` option.

`-ee`										
Set the escape character to `e`. There is no space separating the option letter and the argument character. To start a line with the escape character, two of the escape characters must be entered. The default escape character is tilde (~). Some characters may conflict with your terminal configuration, such as `^S`, `^Q`, or backspace. Using one of these as the escape character may not be possible or may cause problems communicating with the remote host (see stty(1) and tty(7)).

`-l username`								
Set the user login name on the remote host to username. The default name is the current account name of the user invoking rlogin.

# ### Escape Sequences

rlogin can be controlled with two-character escape sequences, in the form `e`x, where `e` is the escape character and `x` is a code character described below. Escape sequences are recognized only at the beginning of a line of input. The default escape character is tilde (~). It can be changed with the `e` option.

The following escape sequences are recognized:

`ey`		If `y` is NOT a code character described below, pass the escape character and `y` as characters to the remote host.

`ee`		Pass the escape character as a character to the remote host.

`e.`		Disconnect from the remote host.

`e!`		Escape to a subshell on the local host. Use `exit` to return to the remote host.

If rlogin is run from a shell that supports job control (see csh(1), ksh(1), and sh-posix(1)), escape sequences can be used to suspend rlogin. The following escape sequences assume that `^Z` and `^Y` are set as the user's susp and dsusp characters, respectively (see stty(1) and termio(7)).

`e^Z`		Suspend the rlogin session and return the user to the shell that invoked rlogin. The rlogin job can be resumed with the fg command (see csh(1), ksh(1), and sh-posix(1)). `e^Z` suspends both rlogin processes: the one transmitting user input to the remote login, and the one displaying output from the remote login.

`e^Y`		Suspend the rlogin session and return the user to the shell