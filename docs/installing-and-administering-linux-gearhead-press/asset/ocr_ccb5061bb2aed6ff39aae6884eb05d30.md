or

```
$ export DISPLAY=sys1:0.0; xterm & <Enter>
```

To accomplish the procedures described in this section and the preceding one, you have to give the systems the capability to allow, restrict, or limit other remote hosts from accessing their displays or applications. To do so, the xhost command must be executed on the server(s).

# ## xhost Command

As mentioned, the X Window System enables users at one host system to run a client on another system. But there might be times, for security or other reasons, when it is not desirable to allow a particular user or system to connect to another. One way to deny access to a user or a system is to use the xhost command on the system to which access is sought.

At the target machine, the user invokes a terminal emulation screen and enters

```
$ xhost [ + | - ] [name] <Enter>
```

The square brackets indicate that the plus and minus signs are optional, as are the usernames or host names. The examples in Table 14.5 should help to clarify these concepts. If you need further information, consult your information sources. Note that using only xhost + will open the machine in question to everyone on the network, and if applicable, possibly to everyone on the Internet. Consequently, if your machine is exposed to a large network or to the Internet, you should install security on the

Table 14.5 xhost Syntax Options

| SYNTAX | EXPLANATION |
| :--- | :--- |
| xhost | Ask for a message: Is access control enabled or not? |
| xhost + | Turn off access control; grant access to everyone. |
| xhost - | Turn on access control; grant access only to those on the list. |
| xhost + name | Add name to the list of users/hosts allowed to connect to this X server (the + is optional here). |
| xhost - name | Delete name from the list of users/hosts allowed to connect to this X server. |