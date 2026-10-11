work file locking with the underlying OS. SGI IRIX and Linux are the only two OSs that are oplock-aware at this time.

Unless your system supports kernel oplocks, you should disable oplocks if you are accessing the same files from both UNIX/Linux and SMB clients. Regardless, oplocks should always be disabled if you are sharing a database file (e.g., Microsoft Access) between multiple clients, because any break the first client receives will affect synchronization of the entire file (not just the single record), which will result in a noticeable performance impairment and, more likely, problems accessing the database in the first place. Notably, Microsoft Outlook’s personal folders (\*.pst) react quite badly to oplocks. If in doubt, disable oplocks and tune your system from that point.

If client-side caching is desirable and reliable on your network, you will benefit from turning on oplocks. If your network is slow and/or unreliable, or you are sharing your files among other file sharing mechanisms (e.g., NFS) or across a WAN, or multiple people will be accessing the same files frequently, you probably will not benefit from the overhead of your client sending oplock breaks and will instead want to disable oplocks for the share.

Another factor to consider is the perceived performance of file access. If oplocks provide no measurable speed benefit on your network, it might not be worth the hassle of dealing with them.

# 16.3.1 Example Configuration

In the following section we examine two distinct aspects of Samba locking controls.

# 16.3.1.1 Disabling Oplocks

You can disable oplocks on a per-share basis with the following:

```
[acctdata]
        oplocks = False
        level2 oplocks = False
```

The default oplock type is Level1. Level2 oplocks are enabled on a per-share basis in the `smb.conf` file.

Alternatively, you could disable oplocks on a per-file basis within the share:

```
veto oplock files = /\*.mdb/\*.MDB/\*.dbf/\*.DBF/
```

If you are experiencing problems with oplocks, as apparent from Samba’s log entries, you may want to play it safe and disable oplocks and Level2 oplocks.

# 16.3.1.2 Disabling Kernel Oplocks

Kernel oplocks is an `smb.conf` parameter that notifies Samba (if the UNIX kernel has the capability to send a Windows client an oplock break) when a UNIX process is attempting