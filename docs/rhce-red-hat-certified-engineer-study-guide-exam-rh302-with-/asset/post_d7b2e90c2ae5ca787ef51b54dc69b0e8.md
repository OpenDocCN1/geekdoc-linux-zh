
## Review Questions

- 1. Which of the following are primary Red Hat Linux desktop environments?
A. AfterStep
B. FVVM
C. GNOME
D. KDE

- 2. Which window manager was the first GNOME-compatible window manager?
A. AfterStep
B. Enlightenment
C. FVVM
D. WindowMaker

- 3. Which window manager is generally used with KDE?
A. AfterStep
B. FVVM
C. KWM
D. WindowMaker

- 4. The utility used to specify the desktop manager is:
A. control-panel
B. switchdesk
C. xdm
D. xinitrc

- 5. If X is started via startx, X will attempt to source which of the following files?
  A. ~/.startx
  B. ~/.xinitrc
  C. ~/.xrc
  D. ~/.Xsession

- 6. To specify that an X client should display red text, which of the following options should be specified?
  A. -background red
  B. -bordercolor red
  C. -font red
  D. -foreground red

## Answers to Review Questions

- 1. C, D. GNOME and KDE are the primary Red Hat Linux desktop environments.

- 2. Enlightenment was the first GNOME-compatible window manager; several other window managers are now more or less GNOME compliant.

- 3. KDE is generally used with KWM.

- 4. The switchdesk utility lets you specify the desktop manager.

- 5. If X is started via startx, it will source the file `~/.xinitrc`, if the file exists.

- 6. D. The -foreground option sets the color of text.

## Configuring and Using Remote X Servers and Clients

RHCE PREPARATION TOPICS COVERED IN THIS CHAPTER:

- Understand and be capable of configuring and using the remote capabilities of X, including remote clients and remote logins.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_686_0.png)

One of the most useful features of X is its support for remote clients and remote logins. Using this feature, you can run an X client on one host and display the client's user interface on another host. For example, you can run a program on a remote supercomputer, yet control the program and view its output via your own desktop. This chapter explains the procedure for configuring and using remote clients and servers.

## X Security

X implements a simple host-based security scheme that prevents unauthorized hosts from accessing an X server. More sophisticated, user-based authentication schemes are also supported.

Host-based X security is configured via the xhost command. You can view the current security settings by issuing the following command:

```
xhost
```

The command will report whether access control is currently enabled or disabled and list the hosts on the access list. For example, the following output indicates that access control is currently disabled and that, if access control were enabled, only the hosts dale and roy could connect:

```
access control disabled, clients can connect from any host
INET:dale
INET:roy
```

## Launching a Remote Client

You can issue the xhost command to query a local or remote X server. Issuing the command remotely lets you verify that the local host has permission to access the remote server, which is identified by the value of the DISPLAY environment. For example, the following commands check the permission of the local host to access the X server running on the host bigger:

```
export DISPLAY=bigger:0.0
xhost
```

Other forms of the xhost command must be executed locally—that is, on the host running the X server. To enable host-based security, issue the command

```
xhost -
```

To disable host security, so that all hosts can access the local X server, issue the command

```
xhost +client
```

To extend permission for a client to access the local X server, issue a command of the form

```
xhost -client
```

where client is the IP address or host name of the client. To deny permission for a client to access the local X server, issue a command of the form

where client is the IP address or host name of the client. The X server stores the IP addresses of hosts, rather than host names, on the access list. Therefore, DNS must be able to perform forward and reverse lookups on any host you specify.

## Launching a Remote Client

Launching a remote client is simple and can be accomplished in any of several ways. One way is to use the display argument provided by most X clients. For example, the following command launches the X client xeyes that runs on the host bigger:

```
xeyes -display bigger:0.0 &
```

Figure 28.1 shows the xeyes client, which displays a pair of eyes that follow the movement of the mouse, in operation.

### FIGURE 28.1 The xeyes Client

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_688_0.png)

The xeyes program doesn't do much. But, for exactly that reason, it's useful for testing and troubleshooting X.

The general form of the command for launching a remote X client is xclient -display server[:m[.n]] [xclient_args]
where:

- xclient and xclient_args are the client and its optional arguments.
- server is the host name or IP address of the server.
- m is the optional display (by default, 0).
- n is the optional screen number (by default, 0).

If you plan to launch several clients, you may find it more convenient to set the DISPLAY variable. Subsequently, when you launch an X client, the value of DISPLAY environment determines the X server that is used. For example, the following sequence of commands launches xeyes and xclock to run on the host bigger; also launches its output locally on the host workstation.

```
```
export DISPLAY=bigger:0.0
xeyes &
xclock &
```

If the X server's authentication feature is active, the client must be authorized to access the server. Otherwise, the client program fails with a message such as:

> Xlib: connection to bigger:0.0 refused by server
Error: Can't open display: bigger.0

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_689_0.png)

Follow the command to launch an X client with ampersand (&) if you want shell to immediately return a new prompt.

Suppose you're currently logged into the host workstation and you want to run a program—say, xterm—on the host server but receive its output locally on the host workstation. The following sequence of commands accomplishes that goal:

```
[user@workstation]$ xhost +server
[user@workstation]$ telnet server
(log in omitted)
[user@server]$ export DISPLAY=workstation:0.0
[user@server]$ xterm &
```

Now complete Exercise 28.1, which gives you experience with host-based security.

## Configuring X Security for Remote Clients

Host-based security does not give a fine degree of control over remote clients, but it's simple to configure and use. To gain experience with host-based security, performing the following steps:

- 1. On a server, enable host-based security so that it excludes some client host.

### EXERCISE 28.1

- 2. From the client host, attempt to log in to the server or open an X window on the server. What happens?

- 3. Without disabling host-based security, extend the client permission to connect to the server.

- 4. From the client host, attempt to log in to the server or open an X window on the server. What happens?

You can perform this exercise on a single computer by running two instances of X. However, you'll likely find it far simpler to use two computers. You can consult this book and other documentation to help you complete this exercise. But, before taking the RHCE exam, be sure you can perform operations such as these without help.

## Configuring Remote Login

In addition to running X clients remotely, you can remotely log to a host that is running an X display manager. The display manager will display a dialog box, such as that shown in Figure 28.2, that lets you specify your login username and password. Some display managers will provide dialog boxes that let you specify the window manager or other options.

### FIGURE 28.2 An X Login dialog box

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_690_0.png)

Copyright ©2000 SYBEX, Inc., Alameda, CA    www.sysex.com
