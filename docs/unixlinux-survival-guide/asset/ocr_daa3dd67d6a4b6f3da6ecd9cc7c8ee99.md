uses the current username if the name part is omitted from the address. If you need to keep the permissions and the ownership of the files, then you would use the -p option. To copy a directory tree, you would use the option -r (recursive), as shown in Listing 7.23.

# LISTING 7.23 Transferring a Directory Tree

```
erikk@unixhost> scp -rp var erikk@192.168.0.2:base_reports/unixhost/.
erikk@192.168.0.2's password:
base_retrans.log.0 100% |**********| 10 00:00
sar_idl_log.040831 100% |**********| 315 00:00
dw_export_home_user 100% |**********| 2 00:00
dw_export_home_user 100% |**********| 3 00:00
dw_export_home_user 100% |**********| 8 00:00
dw_export_home_user 100% |**********| 21 00:00
...
```

The command shown in Listing 7.23 copies the var directory and all subdirectories in it to the system at the IP address 192.168.0.2. If you do not need the display of the transfer in progress, you could use -q (quiet) to suppress it.

As you can see, transfer of data between systems can be done in a secure way by making use of the ssh package. This capability is especially important if you need to transfer configuration files or files containing sensitive data from one system to another. You should avoid using the old, insecure commands like rcp. You never know who is listening in. If you need to transfer files over the Internet, then using insecure commands should be out of the question anyway.

# 7.4.2 Unused Ports and Accounts

Every *NIX system uses ports to channel the data streams between systems and even for communication that is internal to one single system. Ports are used by programs and services to wait for messages. Software that sends out e-mail would use the port number 25 to talk to the mail server process and deliver the mail. If you use a system as mail server, you should not block port 25. But provided there is no firewall to block unused ports, it is a good idea to block all unused ports on a given system. This does not mean you should block everything unknown to you, but at least a list of services you definitely won't use. Listing 7.24 shows examples of unused or not to be used ports.

# LISTING 7.24 Unused Ports

```
...
# FINGERD - finger daemon
```