
# NET NAME

**NET NAME** - This command adds or deletes a messaging name from a computer. This command is not to be confused with **NET USER**, which adds or deletes user accounts on a system.

The following is a summary of the **NET NAME** command.

```
C:\ NET NAME /?
```

```
NET NAME [name [/ADD | DELETE]]
```

Some commonly used options follow:

| **name** | Name to add or delete. |
|---|---|
| **/ADD** | Adds a name to the computer. |
| **/DELETE** | Deletes a name from the computer. |

# NET PAUSE

**NET PAUSE** - Suspends a Windows service.

The following is a summary of the **NET PAUSE** command:

```
C:\ NET PAUSE /?
NET PAUSE service
```

You can pause and continue many Windows services with the **NET PAUSE** and **NET CONTINUE** commands, respectively. The following example shows using the **NET PAUSE** command to pause the **NET LOGON** service and then to restart it with the **NET CONTINUE** command.

Figure 19-3 shows the *Services* dialog box from a system, showing some of the services running on a system.

![](img/75f39fc91296b889c0653851accdfd46_1310_0.png)

**Figure 19-3** *Service Dialog Box with Net Logon Started*

We now use the **NET PAUSE** command to pause the *Net Logon* service:

```
C:\>NET PAUSE NTLOGON
The Net Logon service was paused successfully.
```

Figure 19-4 shows the *Services* dialog box showing that the *Net Logon* service has indeed been paused.

![](img/75f39fc91296b889c0653851accdfd46_1311_0.png)

**Figure 19-4** *Service Dialog Box with Net Logon Paused*

We can now continue the *Net Logon* service with the following NET CONTINUE command:

```
C:\NET CONTINUE NTLOGON

The Net Logon service was continued successfully.
```

# NET PRINT

**NET PRINT** - This command lists print jobs and shared queues.

The following is a command summary of the **NET PRINT** command.

```
C:\ NET PRINT /?

NET PRINT \\computename\sharename
[\\computename\ job# [/HOLD | /RELEASE | /DELETE]]
```

Some commonly used options follow:

- **\\computename**
  The *computename* sharing the print queues.
- **sharename**
  The print queue *sharename*.
- **job#**
  The unique number assigned to a print job.
- **/HOLD**
  The job is assigned a status of *HOLD*, which means that it will not be printed until it is released or deleted.
- **/RELEASE**
  Releases a print job so that it can be printed.
- **/DELETE**
  Deletes a print job from the print queue.

# NET SEND

**NET SEND** - Sends messages to other users, computers, or messaging names on the network.

The following is a summary of the **NET SEND** command.

```
C:\\ NET SEND /?
NET SEND {name | * | /DOMAIN[:name] | /USERS} message
```

Some commonly used options follow:

- **name**
  The user name, computer name, or messaging name to which the message is to be sent. Use quotation marks if there are blank characters in the name.
- **\***
  Use \* to send a message to all users within your group rather than an individual name.
- **/DOMAIN[:domainname]**
  Use /DOMAIN to send a message to all users in the /DOMAIN. You can also specify a domainname to which you want the message sent.
- **message**
  This is the text message you want sent.

The following example shows issuing the NET SEND command to send a message to a specific user:

```
NET SEND marty Our NetServer Lxr has arrived for installation.
```

Figure 19-5 shows the alert box that appears on the screen of the computer on which *marty* is working.

![](img/75f39fc91296b889c0653851accdfd46_1314_0.png)

**Figure 19-5** Alert Box Produced from the NET SEND Command

# NET SESSION

**NET SESSION** - Views or disconnects sessions between computers.

The following is a summary of the **NET SESSION** command.

```
C:\ NET SESSION /?
NET SESSION [\\computername] [/DELETE]
```

Some commonly used options follow:

| **Option** | **Description** |
| :--- | :--- |
| **\\computername** | Lists session-related information for computername. |
| **/DELETE** | Terminates a session between the local computer and computername, closing open files. Without a computername, all sessions are ended. |

# NET SHARE

**NET SHARE** - This command is used to list information about existing shares or to share a server's resources with other network users. The command lists information about existing shares if you don't specify any options.

The following is a summary of the **NET SHARE** command.

```
C:\ NET SHARE /?
NET SHARE sharerame
sharerame=drive:path [USERS:number | /UNLIMITED]
[REMARK:"text"]
sharerame [/USERS:number | /UNLIMITED]
[/REMARK:"text"]
{sharerame | devicename | drive:path} /DELETE
```

Some commonly used options follow:

| **Option** | **Description** |
| :--- | :--- |
| **sharerame** | Network name of the shared resource. Using the *sharerame* only displays information about the share. |
| **devicename** | Used to specify printers to be shared with *sharerame*. Use LP1-LPT9 as a *devicename*. |
| **drive:path** | Use this option to specify that a specific drive and path for a directory are to be shared. |
| **/USERS:number** | Use this option to specify the maximum number of users that can simultaneously access a shared resource. |
| **/UNLIMITED** | An unlimited number of users may simultaneously access a shared resource. |
| **/REMARK:"text"** | Associates a remark with the specified shared resource. |
| **/DELETE** | Sharing is deleted for the specified resource. |

Let’s now use **NET SHARE** to set up a new share on a system. To begin, let’s look at the existing shares using the **NET SHARE** command with no options:

```
D:\ NET SHARE
```

```
Share name    Resource                                Remark
------------------------------------------------------------
ADMIN$        D:\WINNT                                 Remote Admin
IPC$          C:\                                        Remote IPC
C$            C:\                                        Default share
print$        D:\WINNT\system32\spool\drivers            Printer Drivers
D$            D:\                                        Default share
E$            E:\                                        Default share
net_share     C:\net_share
NETLOGON      D:\WINNT\system32\Repl\Import\S            Logon server share
HPLaserJ5     LPT1:                                     Spooled  HP LaserJet 5MP
The command completed successfully.
```

Now we can set up a share of the **c:\\measureware** directory with a sharename of *measure* and a maximum number of five users:

```
C:\ NET SHARE measure=c:\measureware /users:5
measure was shared successfully
```

Issuing the NET SHARE command shows that the share named "measureware" has been established.

```
C:\ NET SHARE

Share name Resource Remark
------------------------- ------------- ----------------------
D$ D:\ Default share
ADMIN$ D:\WINNT Remote Admin
IPC$ C:\ Remote IPC
C$ C:\ Default share
print$ D:\WINNT\system32\spool\drivers Printer Drivers
E$ E:\ Default share
measure c:\measureware
net_share c:\net_share
NETLOGON D:\WINNT\system32\Repl\Import\S Logon server share
HPLaserJ5 LPT1: Spooled HP LaserJet 5MP
The command completed successfully.
```

# NET START

**NET START** - This command starts services that have been stopped using the **NET STOP** command or that have not been started. Issue **NET START** without options to see a list of currently running services.

The following is a summary of the **NET START** command.

```
C:\ NET START /?
NET START [service]
```

The following example shows issuing the **NET START** command without any options to list currently running services:

```
C:/ NET START
These Windows services are started:

    Alertor
    Computer Browser
    EventLog
    FTP Publishing Service
    Gateway Service for NetWare
    Gopher Publishing Service
    License Logging Service
    MeasureWare Agent
    MeasureWare Transaction Manager
    Messenger
    Net Logon
    NT LM Security Support Provider
    OracleServiceTMI
    OracleStartTMI
    OracleTNSListener
    Plug and Play
    Remote Procedure Call (RPC) Locator
    Remote Procedure Call (RPC) Service
    Schedule
    Server
    Spooler
    STP/A - TCP/IP Page Server (TMI)
    TCP/IP NetBIOS Helper
    UPS
    Workstation
    World Wide Web Publishing Service
The command completed successfully.
```
