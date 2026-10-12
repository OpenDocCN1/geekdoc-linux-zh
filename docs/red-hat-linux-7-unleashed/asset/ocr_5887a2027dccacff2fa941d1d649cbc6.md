# # DNS Maps Names to IP Numbers and Vice Versa

DNS maps names to IP numbers and vice versa. That's all it does. This is a vital concept to understand.

Almost everything you can do with a fully qualified domain name, URL, or any other name resolvable to an IP address, you can do with that IP address. And if you use IP addresses, you needn't use DNS (except for a few reverse DNS situations). For the most part, if a command doesn't work with the IP address, the fault is not with DNS but with a lower-level network function. Trying commands with IP addresses instead of domain names and URLs is a great troubleshooting test.

# ## The Forward and Reverse Zones Must Be Kept in Sync

The forward and reverse zones must be kept in sync. If a host changes IP addresses, that fact must be recorded in both the forward and the reverse zone data files and the serial number for each incremented. Failure to keep forward and reverse zones in sync can cause a variety of hard to solve problems, possibly worldwide.

# ## The HUP Signal Versus Restart

According to most literature, including the *named* man page, *named* is forced to reload its zone data files by the following command:

```
`# kill -HUP `cat /var/run/named.pid``
```

Unfortunately, this doesn't always work. A test that doesn't do what the troubleshooter thinks it does can waste hours. Therefore, the recommended way to get the zone data files to reload is with a restart:

```
`# /etc/rc.d/init.d/named restart`
```

Restarting loses accumulated cache and eliminates DNS service during the restart process (20 seconds to 4 minutes). If that is unacceptable, you can try the *HUP* signal, but be very careful to verify that it does what you think it will. You can view the current *named* database and cache by sending *named* an INT signal. This is explained in the section “Troubleshooting DNS,” later in this chapter.

# ## The in-addr.arpa Domain

All reverse mappings exist in the in-addr.arpa domain, thereby eliminating any possible confusion regarding the number's purpose. The network and subnetmask parts of the IP address are placed in reverse order to follow the standard way domain names are