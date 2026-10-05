# nsswitch.conf: WHICH SERVICE TO LOOK AT FIRST

Once NIS and DNS were introduced, finding user and system information was no longer a simple matter of searching a local file. Once you looked in /etc/passwd to get user information and in /etc/hosts to find system address information, now you can use several methods switch to obtain this type of information. /nsswitch.conf (name service switch configuration) specifies files which to use and in order to use them when looking for a certain type of information. You can also specify which action the system should take based on whether a method succeeds or fails.

Syntax Each line in nsswitch.conf specifies how to search for a piece of information, such as a user's password. A line in nsswitch.conf has the following syntax:

```
info:[method [action]] [method [action]]...
```

where info is the type of information the line describes, method is the method used to find the information, and action is the response to the status of the preceding method. The action is enclosed within square brackets.

# How nsswitch.conf Works

When called upon supply information that nsswitch.conf describes, the system examines the line with the appropriate info field. The methods specified on this line, starting with the method on the left. By default, when it finds the desired information, the system stops searching. Without an action specification, when a method fails to return a result, the system tries the next action. It is possible for the search to end without finding the requested information.

# INFORMATION

The nsswitch.conf file completely controls searches for usernames, passwords, host IP addresses, and group information. The following list describes most of the types of information (info in the syntax given earlier) nsswitch.conf controls searches for:

+   - automount Automount (/etc/auto.master and /etc/auto.misc; page 792)
bootstrap Diskless and other booting options (see the bootstrap man page).
ethers MAC address (page 1158)
group Groups of users (/etc/group; page 492)
hosts System information (/etc/hosts; page 493)
networks Network information (/etc/networks)
passwd User information (/etc/passwd; page 494)
protocols Protocol information (/etc/protocols; page 495)
nublickey Used for NFS running in secure mode
rpc RPC names and numbers (/etc/rpc; page 496)
services Services information (/etc/services; page 497)
shadow Shadow password information (/etc/shadow; page 497)