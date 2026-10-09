# **nsswitch.conf: Which Service to Look at First**

Once NIS and DNS were introduced, finding user and system information was no longer a simple matter of searching a local file. When once you looked in /etc/passwd to get user information and in /etc/hosts to find system address information, now you can use several methods to obtain this type of information. The /etc/nsswitch.conf (name service switch configuration) file specifies which methods to use and the order in which to use them when looking for a certain type of information. You can also specify which action the system should take based on whether a method succeeds or fails.

Syntax Each line in nsswitch.conf specifies how to search for a piece of information, such as a user's password. A line in nsswitch.conf has the following syntax:

```
info: method [[action]] [method [[action]]...]
```

where info is the type of information the line describes, method is the method used to find the information, and action is the response to the return status of the preceding method. The action is enclosed within square brackets.

When called upon to supply information that nsswitch.conf describes, the system examines the line with the appropriate info field. It uses the methods specified on this line, starting with the method on the left. By default, when it finds the desired information, the system stops searching. Without an action specification, when a method fails to return a result, the system tries the next action. It is possible for the search to end without finding the requested information.

# Information

The nsswitch.conf file commonly controls searches for usernames, passwords, host IP addresses, and group information. The following list describes most of the types of information (info in the syntax given earlier) that nsswitch.conf controls searches for:

+   - automount Automount (/etc/auto.master and /etc/auto.misc; page 821)
+   - bootparam Diskless and other booting options (bootparam man page)
+   - ethers MAC address (page 1259)
+   - group Groups of users (/etc/group; page 506)
+   - hosts System information (/etc/hosts; page 507)
+   - networks Network information (/etc/networks)
+   - passwd User information (/etc/passwd; page 508)
+   - protocols Protocol information (/etc/protocols; page 510)
+   - publickey Used for NFS running in secure mode
+   - rpc RPC names and numbers (/etc/rpc; page 510)
+   - services Services information (/etc/services; page 511)
+   - shadow Shadow password information (/etc/shadow; page 511)