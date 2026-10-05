# Prioritizing sources of administrative information

# 19.5 PRIORITIZING SOURCES OF ADMINISTRATIVE INFORMATION

Administrative information can be distributed in several ways. Every system understands flat files and knows how to use DNS to look up hostnames and Internet addresses. Since a piece of information could come from several potential sources, there's also a way for you to specify the sources that to be checked and in the order in which they are made.

The /etc/nsswitch.conf (/etc/netsvc.conf on AIX) config files allow an explicit search path to be specified for each type of configuration information. A typical nsswitch.conf file looks something like this:

```
passwd: files ldap
hosts: files dns
group: files
..
```

Each line configures one type of information (usually

Sources are read from left to right until one of them produces an answer for the query. In the example above, the gethostname would first check the /etc/hosts file, and if the host was not listed, then check DNS. Queries about UNIX groups, on the other hand, would check only the /etc/group file.

If necessary, you can define the "failure" of a source more specifically by putting bracketed expressions after it. For, the line

```
hosts: dns [NOTFOUND=return] files
```

causes DNS to be used exclusively if it is available; a negative response from the name server makes queries immediately (with a failure code) without checking flat files. However, flat files are used if no name server is available. The various types of failures are shown in Table 19.5; each can be set to return or continue, signifying whether the query should be aborted or forwarded to the next source.

# Table 19.5 Failure modes recognized in /etc/nsswitch.conf

| Condition | Meaning |
|---|---|
| UNAVAIL | The source does not exist or is down. |
| NOTFOUND | The source exists, but couldn't answer the query. |
| TRYAGAIN | The source exists but is busy. |
| SUCCESS | The source was able to answer the query |

+   6. An ill-supported successor to the original NIS, now discontinued by Sun but still supported by some systems for historical reasons.

![](bbox=[0.94, 0.186, 0.99, 0.276])