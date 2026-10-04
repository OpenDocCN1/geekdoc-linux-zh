
- /cgi-bin/printenv
- /fcgi-bin/echo
- /fcgi-bin/echo2

Before a Web server is introduced to a production environment, all sample pages and scripts should be deleted.

## Defending Oracle

Securing Oracle servers may seem, at first, a daunting task. Because much of Oracle is undocumented, it will be a long time before Oracle could be considered as “secure.” A full investigation is needed; in the process of researching for this chapter, over 22 vulnerabilities were discovered, some of which have been discussed. New vulnerabilities will always be discovered, the best you can do is to mitigate the risk by employing best practices, which are discussed in this section.

## Securing the Listener

If you have already read the section “Attacking Oracle Servers,” you should recognize that the first and most important step to take, as far as securing Oracle is concerned, protecting the Listener. Many of the attacks against the Listener require no user ID and password, and so this will be the first port of call for an attacker looking to break into an Oracle database server.

## Valid Node Checking

It is possible to restrict access to the Listener, and therefore Oracle, by hostname or IP address. Although truth mechanisms based upon such criteria are not foolproof by any stretch of the imagination (because a skilled attacker can bypass it), it does go a long way to help secure the server. The process is known as *valid node checking* and is set by editing the sqlnet.ora file found in the $ORACLE_HOME\network\admin directory in Oracle8i and earlier versions, the file you'll need to edit is the protocol.ora file.

Add the following line:

```
tcp.validnode_checking = YES
```

This will turn on this protection mechanism. Host can be allowed access or specifically denied access. For each host you wish to allow access to, such as the workstation of your DBA and those machines such as Web application servers do require access, add an entry similar to the following:

To deny access to certain hosts, add an entry similar to this:

```
tcp.excluded_nodes = (10.1.1.99)
```

This may be useful if a certain machine is appearing “troublesome” (that is, or your user is attacking your server!). Needless to say, if the attacker were to “take out” an invited machine with a denial of service attack, she could change her IP address and get access. One might wonder why, then, is it worthwhile doing this? Well, the answer lies in the “defense in depth” strategy. By placing hurdles in front of attackers, it will take them to longer to break in, and hopefully in time that you notice something is going on.

## Setting a Listener Password

The Listener can be configured in such a way that many of the administration operations can be remotely controlled require the user to provide a password before change is made. By default, there is no Listener password set, so this is an important step to take as soon as Oracle is installed. To set the Listener password, run the Listener Control Utility, connecting to the relevant listener, and enter the following, substituting password for a suitably strong choice of your own. Doing so will add an entry to the listener.ora file in the $ORACLE_HOME\network\admin directory.

```
LSNRCTL> CHANGE_PASSWORD
Old password: <enter>
New password: password
Reenter new password: password
LSNRCTL> SAVE_CONFIG
```

It is also possible to set the Listener password using the Oracle Net Manager. You can do this from the Authentication tab of a Listener’s General Parameters.

## Admin Restrictions

In addition to locking down the Listener with a password, you can also restrict what operations can be performed remotely if the correct password is supplied. This helps layer security and should be noted. Edit the listener.ora file in the $ORACLE_HOME\network\admin directory and add the following entry:

```
ADMIN_RESTRICTIONS_listener=on
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_737_0.png)

Replace listener with the name of the Listener being protected.

## Remove PL/SQL External Procedures Functionality

Although the extra functionality that is provided by PL/SQL External Procedures is fairly handy it does open a security hole, and attackers may find it more helpful than you do. As such, it is recommended that in most cases you remove it. To do this, edit the listener.ora and tnames.ora files in the $ORACLE_HOME\network\admin directory.

In the listener.ora file, find the section that looks similar to the following:

```
SID_LIST_LISTENER =
(SID_LIST =
(SID_DESC =
(SID_NAME = PLSExtProc
(ORACLE_HOME = C:\ora9ias
(PROGRAM = extproc))
)
(SID_DESC =
(GLOBAL_DBNAME =db.HEPHAESTUS.ngsoftware.com)
(ORACLE_HOME = C:\ora9ias
(SID_NAME = iasdb)
)
)
```

Remove the entry for PLSExtProc:

```
SID_LIST_LISTENER =
(SID_LIST =
(SID_DESC =
(GLOBAL_DBNAME = iasdb.HEPHAESTUS.ngsoftware.com)
(ORACLE_HOME = C:\ora9ias
(SID_NAME = iasdb)
)
)
```

Please note that depending upon how and where you've installed Oracle, the PLSExtProc entry may be iache_extproc or simply extproc. Open the tnsnames.ora file and locate the section that looks similar to the following code and remove it.

```
EXTPROC_CONNECTION_DATA =
(DESCRIPTION =
```
```
(ADDRESS_LIST =
  (ADDRESS = (PROTOCOL = IPC) (KEY = EXTPROCO))
  (CONNECT_DATA =
    (SID = PLSExtProc
      (PRESENTATION = RO)
  ))
```

## Setting the Service Account

The Listener should never run as a high privileged account. On a Unix system, ensure the Listener is running as “nobody,” and on Windows create a guest account and use it. On Windows, you’ll need to assign this account “Logon as a service” privilege. By default, the Listener runs as the powerful SYSTEM account. Based upon the number of buffer overflows found in the Listener in the past, it’s definitely a good idea not to have it running as SYSTEM because this could lead to a complete server compromise.

## Securing the Database

Securing the database involves preventing unauthorized users from accessing the system and preventing unauthorized users from accessing functionality they are not authorized to use.

## Default Passwords

The most basic step in preventing unauthorized access to the database is by ensuring that all default passwords have been reset with strong new passwords. This is accomplished with the following statement:

```
ALTER USER <USERNAME> IDENTIFIED BY <NEW PASSWORD>
```

The following is a list of some of the Oracle username and passwords. This list is growing continuously, so you should seek out other sources to verify a complete list of default database and passwords:

- ADAMS/WOOD
- AQDEMO/AQDEMO
- AQUSER/AQUSER

![](img/729efc56f204a2ebffb8295c3a2dfdfb_739_0.png)

- AURORA$ORB$UNAUTHENTICATED/INVALID
- BLAKE/PAPER
- CATALOG/CATALOG
- CDEMO82/CDEMO82
- CDEMOCOR/CDEMOCOR
- CDEMOUID/CDEMOUID
- BLAKE/PAPER
- CATALOG/CATALOG
- CDEMO82/CDEMO82
- CDEMOCOR/CDEMOCOR
- CDEMOUID/CDEMOUID
- CTXSYS/CTXSYS
- DBSNMP/DBSNMP
- DEDEMO/DEMO
- SCOTT/SCOTT
- SECDEMO/SECDOMO
- SYS/CHANGE_ON_INSTALL
- SYSTEM/MANAGER
- TRACESVR/TRACE
- TSDEV/TSDEV
- TSUSER/TSUSER
- USER0/USER0
- USER1/USER1
- USER2/USER2
- USER3/USER3
- USER4/USER4
- USER5/USER5
- USER6/USER6
- USER7/USER7
- USER8/USER8
- USER9/USER9
- VRR1/VRR1

- ORDPLUGINS/ORDPLUGINS
- ORDSYS/ORDSYS
- OUTLN/OUTLN
- PO/PO
- POWERCARTUSER/POWERCARTUSER
- PRIMARY/PRIMARY
- PUBSUB/PUBSUB
- RE/RE
- RMAIL/RMAIL
- SAMPLE/SAMPLE
- TIGER/TIGER
- SECDEMO/SECDOMO
- SYS/CHANGE_ON_INSTALL
- SYSTEM/MANAGER
- TRACESVR/TRACE
- TSDEV/TSDEV
- TSUSER/TSUSER
- USER0/USER0
- USER1/USER1
- USER2/USER2
- USER3/USER3
- USER4/USER4
- USER5/USER5
- USER6/USER6
- USER7/USER7
- USER8/USER8
- USER9/USER9
- VRR1/VRR1

![](img/729efc56f204a2ebffb8295c3a2dfdfb_741_0.png)

## Applying Patches

In order to properly secure the database instance, it is absolutely critical that you stay current with patches. It is important to stay aware of when a new patch is available and when a new security vulnerability is reported.

## Security Checklist

- Subscribe to Metalink, Oracle Corporation’s support Web site (http://metalink.oracle.com) to gain access to patches and other support information. *Stay current with patches!
- Employ valid node checking to restrict or deny access to the Listener by hostname or IP address.
- Set a Listener password using the Listener Control Utility or Oracle Net Manager.
- Set admin restrictions on the Listener after setting a Listener password.
- Remove PL/SQL External Procedures functionality.
- On a Unix system, ensure the Listener is running as “nobody.” On Windows, create and use a guest account (you’ll need to assign this account the “Logon as a service”privilege).
- To prevent unauthorized access to the database, ensure that all default usernames and passwords have been reset.
