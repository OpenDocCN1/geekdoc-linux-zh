```
192.168.100.6   hub.wine.edu
192.168.200.10  gateway.wine.edu
wine.edu        MX    10   hub.wine.edu
```

# Hosts on the Internet see only the following:

```
10.10.100.10      mail.wine.edu
10.10.100.11      smtp.whiskey.edu
wine.edu          MX    10   mail.wine.edu
wine.edu          MX    20   smtp.whiskey.edu
```

This “split-horizon” DNS configuration prevents Internet mail hosts from attempting mail delivery to `hub.wine.edu`, or from knowing about any of the systems behind the wine.edu firewall. Both schools run exclusively on **sendmail** and AIX.

![](bbox=[0.14, 0.38, 0.88, 0.92])

**Figure 17-1. Network topology**