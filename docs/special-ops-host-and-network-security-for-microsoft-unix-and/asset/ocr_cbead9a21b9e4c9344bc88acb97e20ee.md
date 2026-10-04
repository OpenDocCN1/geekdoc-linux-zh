+   - /cgi-bin/printenv
- /fcgi-bin/echo
- /fcgi-bin/echo2

Before a Web server is introduced to a production environment, all sample pages and scripts should be deleted.

# # Defending Oracle

Securing Oracle servers may seem, at first, a daunting task. Because much of Oracle is undocumented, it will be a long time before Oracle could be considered as “secure.” A full investigation is needed; in the process of researching for this chapter, over 22 vulnerabilities were discovered, some of which have been discussed. New vulnerabilities will always be discovered, the best you can do is to mitigate the risk by employing best practices, which are discussed in this section.

# # Securing the Listener

If you have already read the section “Attacking Oracle Servers,” you should recognize that the first and most important step to take, as far as securing Oracle is concerned, protecting the Listener. Many of the attacks against the Listener require no user ID and password, and so this will be the first port of call for an attacker looking to break into an Oracle database server.

# # Valid Node Checking

It is possible to restrict access to the Listener, and therefore Oracle, by hostname or IP address. Although truth mechanisms based upon such criteria are not foolproof by any stretch of the imagination (because a skilled attacker can bypass it), it does go a long way to help secure the server. The process is known as *valid node checking* and is set by editing the sqlnet.ora file found in the $ORACLE_HOME\network\admin directory in Oracle8i and earlier versions, the file you'll need to edit is the protocol.ora file.

Add the following line:

```
tcp.validnode_checking = YES
```

This will turn on this protection mechanism. Host can be allowed access or specifically denied access. For each host you wish to allow access to, such as the