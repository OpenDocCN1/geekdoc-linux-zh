
The POSIX commands are what really constitute the UNIX and Windows portion of this chapter. I think, however, that covering the other Windows commands gives UNIX system administrators an idea of the type of Windows system administration commands available.

## The Windows Command Line

The whole Windows operating system is based on performing system administration tasks through the graphical user interface. Why, then, would I include a chapter on the command line? Well, many of us have used operating systems for which the lion's share of system administration work takes place at the command line - and old habits die hard.

The purpose of this chapter is to demonstrate some useful commands that are issued at the command line. You can then decide whether using such commands is helpful to the administration of your Windows server or whether you wish to use only the graphical user interface of Windows.

## NET Commands

This section describes some of the **net** commands of Windows. Here is a list of some widely used **net** commands and a brief explanation of each:

- **net accounts**
  Used to maintain the user accounts database.
- **net computer**
  Used to add or delete computers from the domain database.
- **net config server**
  Displays or changes settings for a server service on which the command is executed.
- **net config workstation**
  Displays or changes settings for the workstation service on which the command is executed.
- **net continue**
  Reactivates a Windows service that has been suspended with the **net pause** command.
- **net file**
  Used for network file manipulation, such as listing ID numbers, closing a shared file, removing file locks, and so on.
- **net group**
  Used to add, display, or modify global groups on servers.
- **net help**
  Displays a listing of help options for any net commands.
- **net helpmsg**
  Displays explanations of Windows network messages, such as errors, warnings, and alerts.
- **net localgroup**
  Used to modify local groups on computers.

| Command | Description |
|---|---|
| **net name** | Used to add or delete a "messaging name" at a computer, which is the name to which messages are sent. |
| **net print** | Used to list print jobs and shared queues. |
| **net send** | Sends messages to other users, computers, and "messaging names" on the network. |
| **net session** | Used to list or disconnect sessions between the computer and other computers on the network. |
| **net share** | Shares a server's resources with other computers on the network. |
| **net start** | Used to start services such as *server*. |
| **net statistics** | Displays the statistics log for the local Workstation or Server service. |
| **net stop** | Used to stop services such as *server*. |
| **net time** | Synchronizes the computer's clock with another computer on the domain. |
| **net use** | Displays, connects, or disconnects a computer with shared resources. |
- **net user**
  Creates or modifies user accounts.
- **net view**
  Lists resources being shared on a computer.

The following are brief descriptions of some of the NET commands and examples of using them.

Many of the descriptions include command summaries that were obtained by typing the command name followed by a /?. For instance, to get a command summary for the NET ACCOUNTS command, you would type the following:

```
C:\ NET ACCOUNTS /?
```

You can also get detailed help information by typing HELP and the command name, as shown in the following example:

```
C:\ HELP NET ACCOUNTS
```

### NET ACCOUNTS

**NET ACCOUNTS** - Maintains user account database.

The following is a summary of the **NET ACCOUNTS** command.

```
C:\ NET ACCOUNTS /?
NET ACCOUNTS  [/FORCELOGOFF:{minutes | NO}]  [/MINPWLEN:length]
              [/MAXPWAGE:{days | UNLIMITED}]  [/MINPWAGE:days]
              [/UNIQUEPW:number]  [/DOMAIN]
NET ACCOUNTS [/SYNC]
```

Some commonly used options follow:

- `/DOMAIN` 
  Perform the specified action on the domain controller rather than the current computer.
- `/FORCELOGOFF` 
  Line numbers are displayed, along with output lines.
- `/MINPWLEN:length` 
  Specify the minimum number of characters for a password with *length*.
- `/MAXPWAGE:days` 
  Specify the maximum number of *days* a password is valid, or use the *unlimited* option to specify no limit on password validity.
- `/MINPWAGE:days` 
  Specify the minimum number of *days* that must pass before a user is permitted to change their password.
- `/UNIQUEPW:number`
  A user password must be unique for the number of changes specified by *number*.
- `/SYNC`
  Synchronize the account database.

The following example shows **NET ACCOUNTS** with no options specified:

```
C:\ NET ACCOUNTS

Force user logoff how long after time expires?:	Never
Minimum password age (days):	0
Maximum password age (days):	42
Minimum password length:	0
Length of password history maintained:	None
Lockout threshold:	Never
Lockout duration (minutes):	30
Lockout observation window (minutes):	30
Computer role:	BACKUP
Primary Domain controller for workstation domain: \\NISDEV

The command completed successfully.
```

We'll now issue **NET ACCOUNTS** with the *MINPWLEN* option to change the minimum password length to five characters:

```
C:\ NET ACCOUNTS /MINPWLEN:5

The request will be processed at the primary domain controller for domain NSDNS

The command completed successfully.
```

Reissuing **NET ACCOUNTS** with no options reflects the new minimum password length:

```
C:\ NET ACCOUNTS

Force user logoff how long after time expires? Never
Minimum password age (days): 0
Maximum password age (days): 42
Minimum password length: 5
Length of password history maintained: None
Lockout threshold: Never
Lockout duration (minutes): 30
Lockout observation window (minutes): 30
Computer role: BACKUP
Primary Domain controller for workstation domain: \\NISDEV
The command completed successfully.
```

### NET COMPUTER

**NET COMPUTER** - Adds or deletes computers from the domain database.

The following is a summary of the **NET COMPUTER** command:

```
C:\ NET COMPUTER /?  
NET COMPUTER \\ computername ({/ADD | /DEL})
```

Some commonly used options follow:

- `\\ computername`
  Name of the computer to be added or deleted.
- `/ADD`
  Add the computer.
- `/DEL`
  Delete the computer.

The following example shows adding a computer using the /ADD option:

```
C:\ NET COMPUTER \\SYSTEM2 /ADD

The request will be processed at the primary domain controller for domain NSDNIS.

The command completed successfully.
```

### NET CONFIG SERVER

**NET CONFIG SERVER** - As a member of Administrator's group, you can change the settings for a service.

The following is a summary of the **NET CONFIG SERVER** command.

```
C:\ NET CONFIG SERVER /?
NET CONFIG SERVER [ /AUTODISCONNECT:time]
[/SRVCOMMENT:"text"]
[/HIDDEN: {YES | NO}]
```

Some commonly used options follow:

- *AUTODISCONNECT:time*
  Use *time* to specify the number of minutes that pass before an inactive account is disconnected.
- *SRVCOMMENT:"text"*
- *HIDDEN: {YES|NO}*

### NET CONTINUE

**NET CONTINUE** - Reactivates a Windows service that had been suspended with **NET PAUSE**.

The following is a summary of the **NET CONTINUE** command.

```
C:\> NET CONTINUE /?
NET CONTINUE service
```

You can pause and continue many Windows services with the **NET PAUSE** and **NET CONTINUE** commands, respectively. The following example shows using the **NET PAUSE** command to pause the **NET LOGON** service and then restart it with the **NET CONTINUE** command.

Figure 19-1 is the *Services* dialog box from a system, showing some of the services running on a system.

![](img/75f39fc91296b889c0653851accdfd46_1297_0.png)

Figure 19-1 Service Dialog Box with Net Logon Started

We’ll now use the **NET PAUSE** command to pause the *Net Logon* service:

```
C:\NET PAUSE NtLOGON

The Net Logon service was paused successfully.
```

Figure 19-2 shows the *Services* dialog box showing that the *Net Logon* service has indeed been paused.
