The `xhost` command can also be used to see if you are allowed to display clients on a remote system. This is done by changing the `DISPLAY` variable to that of the remote host and then running `xhost`. For example, to see if you can display applications on `redhat.the-nashes.net` you would type:

```
export DISPLAY=redhat.the-nashes.net:0.0
xhost
```

The `DISPLAY` variable is covered in detail in the next section.

The `xhost` command uses a few simple command-line options. To enable host-based authentication and clear any allowed hosts you would use `xhost -`. For example:

```
[root@redhat /root]# xhost -
access control enabled, only authorized clients can connect
```

To disable all authentication and allow anyone to connect to your system and display applications, you type `xhost +`. For example:

```
[root@redhat /root]# xhost +
access control disabled, clients can connect from any host
```

> Caution Running `xhost +` is a bad idea, since any user can connect to your X server.

Authorizing hosts to connect is done with the `+` option too. For example, to allow three hosts to connect you would type the following:

```
[root@redhat /root]# xhost +dedee +marvin +brain
dedee being added to access control list
marvin being added to access control list
brain being added to access control list
```

To remove a host from the allowed list you would use the `-` option. For example, to remove `dedee` you would type the following:

```
[root@redhat /root]# xhost -dedee
dedee being removed from access control list
```

Finally, to make sure your authentication is correct, just type `xhost`:

```
[root@redhat /root]# xhost
access control disabled, clients can connect from any host
INET:brain
INET:marvin
```

> Exam Tip The host authentication method is configured using the `xhost` command.