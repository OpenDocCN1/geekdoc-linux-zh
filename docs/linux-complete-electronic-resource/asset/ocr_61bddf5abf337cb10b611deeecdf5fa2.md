due to temporary name server problems. A network address will be unavailable when the software cannot figure out what type of network it is talking to.

**KNOWN** Matches any user whose name is known, and matches any host whose name *and* address are known. This pattern should be used with care: host names may be unavailable due to temporary name server problems. A network address will be unavailable when the software cannot figure out what type of network it is talking to.

**PARANOID** Matches any host whose name does not match its address. When `tcpd` is built with `-DPARANOID` (default mode), it drops requests from such clients even before looking at the access control tables. Build without `-DPARANOID` when you want more control over such requests.

# OPERATORS

**EXCEPT** Intended use is of the form: '`list_1` EXCEPT `list_2`'; this construct matches anything that matches `list_1` unless it matches `list_2`. The EXCEPT operator can be used in `daemon_lists` and in `client_lists`. The EXCEPT operator can be nested: if the control language would permit the use of parentheses, ‘`a` EXCEPT `b` EXCEPT `c`’ would parse as ‘(`a` EXCEPT `b`) EXCEPT `c`)`.

# SHELL COMMANDS

If the first-matched access control rule contains a shell command, that command is subjected to `%<letter>` substitutions (see next section). The result is executed by a `/bin/sh` child process with standard input, output and error connected to `/dev/null`. Specify an `&`' at the end of the command if you do not want to wait until it has completed. Shell commands should not rely on the `PATH` setting of the inetd. Instead, they should use absolute path names, or they should begin with an explicit `PATH=whatever` statement. The `hosts_options(5)` document describes an alternative language that uses the shell command field in a different and incompatible way.