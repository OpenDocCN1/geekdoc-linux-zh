**Syntax:** `MinSpareServers number`

**Default setting:** `MaxSpareThreads` 5 (for Perchld MPM) or 250 (for threaded MPM)

**Context:** Server config

The `perchild` MPM handles idle thread count on a per child basis; thus, when a child has less than the number of minimum threads specified here, the server creates new threads within that child process.

# SendBufferSize

The `SendBufferSize` directive sets the TCP send buffer size to the number of bytes specified. On a high-performance network, setting the directive to a higher value than the operating system defaults may increase server performance.

**Syntax:** `SendBufferSize bytes`

**Default setting:** None

**Context:** Server config

# StartServers

The `StartServers` directive sets the number of child Apache server processes that are created on startup. The number of Apache child processes needed for a certain time period is dynamically controlled. The primary Apache server (the daemon process) launches new child processes as it encounters higher request loads. The actual number of child processes is controlled by the `MinSpareServers`, `MaxSpareServers`, and the `MaxClients` directives. Therefore, you have little to gain by adjusting this parameter.

**Syntax:** `StartServers number`

**Default setting:** `StartServers` 5

**Context:** Server config

> **Note**
> 
> The `StartServers` directive is useful only when the Apache server is running as a standalone server. In other words, you need to have `ServeType` set to standalone for this directive to be effective.

> **Note**
> 
> When running Microsoft Windows, this directive sets the total number of child processes running. Because the Windows version of Apache is multithreaded, one process handles all the requests. The rest of the processes are held in reserve until the primary process dies.