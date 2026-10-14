+   - On a host in another network, through either TCP/IP, DECnet, or UUCP addressing

Use the following syntax for the mailx command:

```
`mailx user [@ { host | domain | host.domain}] ...`
```

To send mail to users on the local host, enter the mailx command and specify a user parameter for each user. For users on remote hosts, you must specify additional information about the location of the host after the “at sign” (@).

For example, to send mail from host orange to users smith and jones on the same local host, you would enter the following command:

```
`orange% mailx smith jones`
```

To send mail to user hobbes on a different host, pluto, in the same **domain**, you would enter the following command:

```
`orange% mailx hobbes@pluto`
```

In the preceding example, if user hobbes were in another domain called planets, you would add the name of the remote network domain, as shown in the following command:

```
`orange% mailx hobbes@pluto.planets`
```

The domain is sometimes split into further subdivisions with the name of each separated by a period (.) in the destination name. Depending on how the network has been configured by the network administrator, you can address a user on a remote host in another domain by specifying only the domain name, as in the following command:

```
`orange% mailx hobbes@planets`
```

If necessary, see your system administrator for help addressing a mail message.

# 11.2 Sending a Mail Message Using mailx

This section explains how to use mailx to send a message to a user on a local host and a copy of the message to other users. To begin the example, user Jones enters the mailx command at the local system prompt, orange%:

```
`orange% mailx suzuki  Return`
```

After pressing the Return key, the Subject: prompt is displayed. Pressing the Return key again immediately would leave the subject blank. Instead, user Jones enters the subject of the message before pressing the Return key, and then begins writing the message:

```
`Subject: Baseball question  Return`
```