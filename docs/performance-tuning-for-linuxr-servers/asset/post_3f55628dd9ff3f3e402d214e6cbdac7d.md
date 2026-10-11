
# Different Models of Web Servers

Like many other servers, web servers have certain performance requirements that affect how the server is implemented. Several possibilities are available for the architectural model that the server is implemented with. One of the major issues is how the server handles *concurrency*. Web servers are required to handle many clients simultaneously, sometimes up to tens of thousands of clients. In the previous example, the server deals with only one client at a time. For example, if the file that the client requests is not in the server's file cache, the server *blocks* waiting for the file to be loaded from disk. During this time, the server could be handling other requests that may be less expensive to serve, but the previous example instead waits, wasting cycles. In addition, because the previous example uses a single process, if the server is an SMP, other processors are completely underutilized. The typical approach to dealing with this problem is through some form of concurrency mechanism; we describe several approaches in this section.

The most common form of concurrency is using processes. The most popular web server, Apache, was originally implemented using processes. Each process has a separate address space and is fully protected and isolated from other processes through a virtual machine abstraction. By assigning each request to a separate process, one process can make forward progress while another is blocked on another activity (such as waiting for a client or disk). In addition, on an SMP, multiple processes can run in parallel. The disadvantage of processes is that they are relatively expensive abstractions to use, requiring resources such as memory to be allocated to them. If a server has thousands of clients, it may have thousands of processes, which can tax a system's resources. Typically, any system is limited in the number of processes it can have active.

The next most common approach is using threads. Apache 2.0 provides the option of using threads rather than processes. Threads are similar to processes but are lighter-weight; namely, they require fewer system resources. Threads typically share address spaces but have separate program counters and stacks. Threads are cheaper than processes but trade protection for speed. In addition, systems can run on resources even using threads, given a large enough number of clients.

Many research web servers, such as the Flash web server from Rice University (not to be confused with Macromedia's Flash browser plug-in), use something called the event-driven model. In this model, a single process is used, without threads, and connections are managed using a multiplexing system call such as `select()` or `poll()`. The server queries the readiness of all connections using the system call and determines which connections require service (and, conversely, which are idle). The server then reads requests or writes responses as appropriate for that particular connection. The advantage of the event-driven model is that it is typically faster than process- or thread-based servers, because it maximizes locality and has many performance optimizations not available to these other models. The disadvantage is that it is more difficult to program, because the developer must explicitly manage state for many requests, each of which can be in a different stage of progress. In addition, operating system support for interacting with the disk in this model (namely, asynchronously) has been historically absent in Linux. However, with the introduction of asynchronous I/O in Linux 2.6, this limitation is being remedied.

The final architectural model we consider here is the in-kernel model. Examples include Red Hat's Tux server and IBM's AFPA server. In this approach, the entire web server is run as a set of kernel threads, rather than in user space. The advantages of this approach are that performance is maximized (because sharing is easy), data copies are avoided, and no expensive user-kernel crossings are incurred. The disadvantages are that kernel programming is more difficult, less portable, and more dangerous than user-space programming. For example, if the server has a programming error and crashes, an in-kernel server could take down the whole machine with it.

## Tuning Web Servers

Many of the approaches to tuning other servers given in other chapters are appropriate for web servers as well. For example, increasing the size of the send and receive socket buffers via `sysctl` or `setsockopt`, as described in Chapter 12, “Network Tuning,” is useful. Similarly, increasing the size of the accept queue helps prevent requests from being dropped by the operating system before the web server even sees them. In this section, we focus on tuning that is done for web servers in particular. This is in addition to tuning that is done on the operating system.

### Tuning for All Web Servers

These changes are useful for all web servers, regardless of the architectural model.

The following parameter increases the number of TCP SYN packets that the server can queue before SYNs are dropped:

```
echo 30000 > /proc/sys/net/ipv4/tcp_max_syn_backlog
```

Web servers typically have a large number of TCP connections in the TIME-WAIT state. The following parameter increases the number of connections that are allowed in that state:

```
echo 2000000 > /proc/sys/net/ipv4/tcp_max_tw_buckets
```

The following parameter sets the length for the number of packets that can be queued in the network core (below the IP layer). This allows more memory to be used for incoming packets, which would otherwise be dropped.

```
echo 50000 > /proc/sys/net/core/netdev_max_backlog
```

### Apache

Apache’s main configuration file is `httpd.conf`. Several parameters can be modified in that file to improve performance:

The following parameter sets the upper bound on the number of processes that Apache can have running concurrently:

```
MaxClients 150
```

Larger values allow larger numbers of clients to be served simultaneously. Very large values may require Apache to be recompiled. This change should be used with care, because large numbers of processes can cause excessive overhead.

The following parameter indicates the number of requests that a single Apache process will perform on a connection for a client before it closes the connection:

```
MaxKeepAliveRequests 100
```

Opening and closing connections consumes CPU cycles, so it is better for the server to provide as many responses on a single connection as possible. Therefore, larger numbers are better. In fact, setting this value to 0 indicates that the server should never close the connection if possible.

The following parameter determines the number of requests an individual Apache process will serve before it dies (and is re-forked). 0 implies that the number is unlimited, but on some systems with memory leaks in the operating system, setting this to a nonzero value keeps the memory leak under control.

```
MaxRequestsPerChild 0
```

The following parameters determine the minimum and maximum number of idle processes that Apache keeps in anticipation of new requests coming in:

```
MinSpareServers 5
MaxSpareServers 10
```

The idea is that it is cheaper to keep a live process idle than to fork a new process in response to a new request arrival. For highly loaded sites, you might want to increase these values.

### Flash and Other Event-Driven Servers

A common problem event-driven servers have is that they use a large number of file descriptors and thus can run out of these descriptors if the maximum is not increased.

The following is an `sh` (shell) command that increases the number of open files a process may have:

```
ulimit -n 16384
```

The process (in this case, the web server) must also be modified to take advantage of large numbers of descriptors:

```
#include <bits/types.h>
#undef __FD_SETSIZE
#define __FD_SETSIZE 16384
```

The default `FD_SETSIZE` on Linux 2.4 is only `1024`.

### Tux

The following parameter determines the number of active simultaneous connections:

```
echo 20000 > /proc/sys/net/tux/max_connect
```

The following parameter sets the maximum number of connections waiting in Tux's accept queue:

```
echo 8192 > /proc/sys/net/tux/max_backlog
```

The following parameter disables logging of requests to disk:

```
echo 0 > /proc/sys/net/tux/logging
```

# Performance Tools for Evaluating Web Servers

Many tools are available for evaluating the performance of web servers, also known as *workload generators*. These are programs that run on client machines, emulating a client's behavior, constructing HTTP requests, and sending them to the server. The workload generator can typically vary the volume of requests it generates, called *load*, and measures how the server behaves in response to that load. Performance metrics include items such as request latency (how long it took an individual response to come back from the server) and throughput (how many responses a server can generate per second).

Perhaps the most commonly used tool is SPECWeb99. This tool is distributed by the Standard Performance Evaluation Corporation (SPEC) nonprofit organization, whose
