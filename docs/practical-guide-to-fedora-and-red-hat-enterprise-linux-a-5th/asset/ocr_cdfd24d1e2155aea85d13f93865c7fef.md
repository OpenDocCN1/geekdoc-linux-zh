where **num** is the maximum number of child processes (servers) Apache runs at one time, including idle processes and those serving requests. When Apache is running **num** processes and there are no idle processes, Apache issues *Server too busy* errors to new connections; it does not start new child processes. A value of 150 is usually sufficient, even for moderately busy sites.

Context: **server config**
Default: 256
Fedora/RHEL: 256

# **MaxRequestsPerChild**

*Specifies the maximum number of requests a child process can serve.*

**MaxRequestsPerChild num**

where **num** is the maximum number of requests a child process (server) can serve during its lifetime. After a child process serves **num** requests, it does not process any more requests but dies after it finishes processing its current requests. At this point additional requests are processed by other processes from the server pool.

Set **num** to 0 to not set a limit on the number of requests a child can process, except for the effects of MinspareServers. By limiting the life of processes, this directive can prevent memory leaks from consuming too much system memory. However, setting MaxRequestsPerChild to a small value can hurt performance by causing Apache to create new child servers constantly.

Context: **server config**
Default: 10000
Fedora/RHEL: 4000

# **MaxSpareServers**

*Specifies the maximum number of idle processes.*

**MaxSpareServers num**

where **num** is the maximum number of idle processes (servers) Apache keeps running to serve requests as they come in. Do not set this number too high, as each process consumes system resources.

Context: **server config**
Default: 10
Fedora/RHEL: 20

# **MinSpareServers**

*Specifies the minimum number of idle processes.*

**MinSpareServers num**

where **num** is the minimum number of idle processes (servers) Apache keeps running to serve requests as they come in. More idle processes occupy more computer resources; increase this value for busy sites only.

Context: **server config**
Default: 5
Fedora/RHEL: 5