```
[global]
windbind uid = 1000-24999
windbind gid = 25000-29999
security = domain
password server = Primary Domain Controller, Backup Domain Controller(s)
```

These two directives control UIDs and GIDs assigned to accounts on the domain controller. If you are attempting to use NIS(+) in conjunction with windbind, be very sure that the ranges you specify for windbind do not interfere with UIDs and GIDs assigned in the NIS tree. If you do, you will get weird results and corrupt your security model.

If plan allow home directories on the Linux box while using windbind, you will be responsible for their creation prior to the user logging. The template home directive in the global section will provide a way of automatically determining the user's home directory will be located. Also, if you plan to use windbind, the default login shell is /bin/false. If your Windows users have any reason to log to the Linux box via Telnet or SSH (SSH is preferred), this parameter shell will need to be changed.

To enable the use of windbind, you will need to modify the /etc/nsswitch.conf file to resemble the following:

+   passwd: files windbind
group: files windbind

In order, a local user will have precedence over one with the same name that appears on the domain controller. If you wish the domain account to have precedence over a local account, simply reverse the files and windbind order.

Another consideration about the windbind daemon running on multiple Samba servers is that if you configure them exactly in the same way, the Linux UIDs and GIDs for the domain accounts are almost guaranteed not to match. Example: we have two Samba servers, SAMBA1 and SAMBA2. Both are running the windbind daemon and authenticating against NTPDC. Larry has an account on the domain controller. On SAMBA1, his Linux UID = 1000, and on SAMBA2, his Linux UID = 1547. There is no way have figured out to automatically fix this. This becomes a real issue if you are attempting to use windbind with any other protocol, especially NFS, which requires synchronization between the UIDs and GIDs of the different Linux computers to ensure good file quality.

Another issue when using windbind to establish user accounts should be noted here. It is far easier to break into Windows computers than a secured Linux computer. Consider this when using a Windows box to provide user accounts for a Linux box. If using windbind, my recommendation is not to have a default shell for any account that is provided by the domain controller.

The association between Windows domain accounts names and their UID is stored in the /var/lock/samba (or wherever you specified) directory. Similarly, the associations between Windows domain groups, their Linux UID, and their membership lists are also controlled and cached in a database file. The caching is necessary to deal with potential network troubles and Microsoft's legendary reliability.