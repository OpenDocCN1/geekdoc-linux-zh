Each of these commands is typed in after the UNIX prompt, and each is terminated by a **Return**. `host` represents the address of the remote host.

# **Remote Login Commands (UNIX shell prompt)**

`rlogin host`     log into a remote UNIX computer named `host`
`telnet host`     log into a remote computer named `host`
`telnet`          start up the `telnet` program

# **Telnet Commands (Telnet Prompt)**

`open host`      open connection to computer `host`
`?`              print `telnet` help
`close`          close connection to remote host
`quit`           quit `telnet` session

+   1. If you have an account on a remote UNIX machine, log into that account using `rlogin`.
+   2. If you have an account on a non-UNIX machine that is connected to the network, log into that account using `telnet`.
+   3. Use `telnet` to log into NASA’s “Spacelink” public server. What kinds of information are available on this server?
+   4. Use `telnet` to log into the geographic server at the University of Michigan. What kind of information is available concerning the city or town where you live?