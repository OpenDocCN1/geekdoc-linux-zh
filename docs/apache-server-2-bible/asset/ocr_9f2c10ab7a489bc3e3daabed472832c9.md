# RLimitPROC

The `RLimitPROC` directive sets the maximum number of simultaneous Apache children-spawned processes per user ID.

Syntax: `RLimitPROC n [ 'max' [ n | 'max'] ]`
Default setting: Not set; uses operating system defaults
Context: Server config, virtual host

The `RLimitPROC` directive takes two parameters. The first parameter sets the soft resource limit for all processes, and the second parameter, which is optional, sets the maximum resource limit. Raising the maximum resource limit requires that the server be running as *root* or in the initial startup phase. For each of these parameters, there are two possible values:

+   * `n` is the number of bytes per process
+   * `max` is the maximum resource limit allowed by the operating system

> **Note**
> If your CGI processes are run under the same user ID as the server process, use of `RLimitPROC` limits the number of processes the server can launch (or 'fork'). If the limit is too low, you will receive a “Cannot fork process” type of message in the error log file. In such a case, you should increase the limit or just leave it as the default.

# UseCanonicalName

The `UseCanonicalName` directive sets how Apache constructs self-referencing URLs. When set to `on`, Apache uses *ServerName* and *Port* directive settings to create the self-referencing URL. If `UseCanonicalName` is set to `off`, then Apache uses the client-supplied *host name* and *port number* from the header information to construct the self-referencing URL. Finally, if `UseCanonicalName` is set to `dns`, Apache will perform a reverse DNS lookup on the server’s IP address to determine the host name for the self-referencing URL. This option is not recommended because the reverse DNS lookup will slow down the request processing.

Syntax: `UseCanonicalName On | Off | dns`
Default setting: `UseCanonicalName On`
Context: Server config, virtual host, directory
Override: Options

# Using dynamic modules

Apache loads all the precompiled modules when it starts up; however, it also provides a dynamic module loading and unloading feature that may be useful on certain occasions. When you use the following dynamic module directives, you can change the list of active modules without recompiling the server.