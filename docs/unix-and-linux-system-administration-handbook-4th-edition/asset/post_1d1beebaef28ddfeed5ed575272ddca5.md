
It’s common to put the best and closest name server first in the nameserver lines, but if you want to load balance between equally competent name servers, you should use the rotate option. For example:

```
options rotate timeout:2 attempts:2
```

rotates between the listed name servers, times out in 2 seconds, and queries each server at most twice.

![](img/14d78e3cecac4581d37024baf1e94cca_610_0.png)

HP-UX does not fully support the options clause illustrated above; the timeout and number of retries variables are set directly in resolv.conf as follows:

```
retrans timeout-value-in-milliseconds
retry #-of-attempts
```

Most resolvers allow you to list a maximum of three name servers. If you list more, they are silently ignored. Table 17.2 summarizes the defaults.

**Table 17.2 /etc/resolv.conf defaults**

| OS | Max NS | Max search length | Timeout | Retries |
|---|---:|---|---|---:|
| Linux | 3 | 6 domains, 256 chars | 5 sec | 2 |
| Solaris | 3 | 6 domains, 256 chars | 5 sec | 2 |
| HP-UX | 3 | 6 domains, 256 chars | 5 sec | 4 |
| AIX | 3 | 6 domains, 1024 chars | 5 sec | 2 |

If a host is itself a name server, it should be listed first in its own **resolv.conf** file. If no name servers are listed, localhost is assumed.

The **resolv.conf** file also understands the domain directive as an alternative to search; it specifies a single domain to add to names that are not fully qualified. It’s an older form; we recommend replacing domain directives with search directives when you encounter them. The directives are mutually exclusive, so only one should be present. If you inadvertently include both directives, only the last one listed takes effect.

![](img/14d78e3cecac4581d37024baf1e94cca_610_1.png)

If there is no **/etc/resolv.conf** file, AIX uses **/etc/netsvc.conf** to decide how to perform name resolution and extracts the default domain name from the host-name, which must be fully qualified. AIX provides a sample **resolv.conf** file in **/usr/lpp/tcpip/samples/resolv.conf** that you can copy. Just in case adding a couple of lines to a text file is too hard for you, AIX provides the **namerslv** command as an interface for adding, deleting, and changing name servers in **resolv.conf**. But wait! You also get the **mknamsv**, **rmnamsv**, **chnamsv**, and **lsnamsv** commands as high-level interfaces to **namerslv**. (Of course, a sysadmin can’t be expected to master a sophisticated set of tools like this overnight, so you’ll probably need a GUI to start out with; try **smitty resolv.conf**.)

Once /etc/resolv.conf has been configured, the system will start using DNS for name service as long as DNS hasn’t been disabled in the file that prioritizes sources of administrative data (/etc/nsswitch.conf, or /etc/netsvc.conf on AIX; see page 739).

After configuring /etc/resolv.conf, you should be able to refer to other machines by name rather than by IP address. Try ping hostname. If you try to reach another local machine and the command just hangs, try referring to the machine by its IP address. If that works, then your DNS configuration is the problem. Verify that the name server IP addresses in /etc/resolv.conf are correct and that the servers you point to allow queries from your network (see page 606). dig from a working machine can answer these questions.

## 17.4 NAME SERVERS

A name server performs several chores:

- It answers queries about your site’s hostnames and IP addresses.
- It asks about both local and remote hosts on behalf of your users.
- It caches the answers to queries so that it can answer faster next time.
- It transfers data between your name servers to keep them synchronized.

Name servers deal with zones, where a “zone” is essentially a domain minus its subdomains. You will often see the term “domain” used where “zone” is what’s really meant, even in this book.

The NSD/Unbound suite separates the function of answering queries about your hosts (the NSD part) from the function of issuing queries about other domains on behalf of your users (the Unbound part). This separation is healthy.

Name servers can operate in several different modes. The distinctions among them fall along several axes, so the final categorization is often not very tidy. To make things even more confusing, a single server can play different roles with respect to different zones. Table 17.3 on the next page lists some of the adjectives used to describe name servers.

These categorizations are based on the name server’s source of data (authoritative, caching, master, slave), on the type of data saved (stub), on the query path (forwarder), on the completeness of answers handed out (recursive, nonrecursive), and finally, on the visibility of the server (distribution). The next few sections provide some additional details on the most important of these distinctions; the others are described elsewhere in this chapter.

### Authoritative and caching-only servers

Master, slave, and caching-only servers are distinguished by two characteristics: where the data comes from and whether the server is authoritative for the domain. BIND can be all three types, NSD can be a master or slave, and Unbound is caching-only.
