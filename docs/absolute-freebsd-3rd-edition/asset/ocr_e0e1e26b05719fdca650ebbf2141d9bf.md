easy to use. The average FreeBSD administrator can use PF to achieve almost any effect possible with the other two packet filters.

> NOTE
> For in-depth discussion of PF, you might check out Peter N. M. Hansteen's The Book of PF (No Starch Press, 2014) or my book Absolute OpenBSD (No Starch Press, 2013), which contains several chapters about PF. You might also look at the online PF FAQ, but that has fewer baiku.

# Enabling PF

PF includes the packet filtering kernel module, pf.ko, and the userland program pfctl(8). Before using PF, you must load the kernel module. The simplest way is to enable PF in rc.conf:

```
pf_enable="YES"
```

PF defaults to the accept all stance, which means that you won't lock yourself out of your server merely by enabling the firewall.

# Default Accept and Default Deny in Packet Filtering

The security stances (default accept and default deny) are critical in packet filtering. If you use the default accept stance and want to protect your system or network, you need numerous rules to block every possible attack. If you use the default deny stance, you must explicitly open holes for every little service you offer. In almost all cases, default deny is preferable; while it can be more difficult to manage, its increased security more than makes up for that difficulty.

When using a default deny stance, it's very easy to lock yourself out of remotely accessing your machine. When you have an SSH connection to a remote machine and accidentally break the rule that allows SSH access, you're in trouble. Everybody does this at least once, so don't be too embarrassed when it happens to you. The point is, it's