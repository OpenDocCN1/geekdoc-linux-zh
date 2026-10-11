Example 10-51 Log Entries Associated with Example 10-50
    Apr 15 12:08:40 topcat xinetd[1402]: FAIL: login address from=19.152.1.5
    Apr 15 12:08:52 topcat xinetd[1402]: FAIL: login address from=19.152.1.5
    Apr 15 12:12:49 topcat xinetd[1402]: FAIL: login address from=19.152.1.5

on page 243. This is because the remote host, sly.no.good.org, is not running the `identd` or similar daemon (maybe Joe is up to something!). Because the host `sly.no.good.org` is not in the `only_from` list in Example 10-47, even if we added the entire `flags` to `ONLY` to the login service entry, it would not record the fact that `sly.no.good.org` is not running `identd`. Such a log record will occur only if the host is allowed.

There is one last log entry to examine. Note that the attribute `instances` is set to 8 in Example 10-47. What happens to the ninth login session? When the ninth user attempts to `rlogin` to topcat, that user will see the following error message:

```
rcmd: topcat: Address already in use
```

and the log entry recorded on `topcat` for this event will be
    Apr 15 13:37:33 topcat xinetd[1402]: FAIL: login service_limit
    from=172.17.55.124

Comparing this record to the description given in Table 10.14, the `FAIL` keyword is followed by the service, then an explanation for the failure (service_limit in this case), and finally the client address.

# Using the bind attribute. The bind attribute allows for associating a particular service with a specific interface's IP address. Suppose we have an internal `ftp` server that supplies read-only resources for company employees via anonymous `ftp` (see Internet Services Resources on page 255 for more details regarding services such as `ftp`). Further suppose that this `ftp` server has two interfaces—one that attaches to the corporate environment and the other that connects to a private internal network that is generally accessible only to employees who work in that particular group. While there are a number of things that need to be done to secure this server (`ipchains` being one; see Chapter 16), we will consider only the requirement to provide two different `ftp` services based on interfaces in this example. Example 10-52 shows two `ftp` service entries in `/etc/xinetd.conf` that would implement the desired functionality. Again, the `defaults` section is provided for completeness.

Notice that each of the two `ftp` service entries has a unique `id` attribute (see Table 10.10 on page 232). There is no limit to the number of services with the same name as long as each has a unique identifier. In this case, we set the `id` attribute to `ftp` for the internal `ftp` server and `ftp_chroot` for the external anonymous server. Note that in the latter case the daemon invoked is `/usr/sbin/anon/in.aftp` (this is the effective equivalent to `twist` for TCP_wrappers), which is different from the former service.