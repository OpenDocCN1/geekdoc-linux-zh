
If the client application happens to be running on the same machine as the X server, you can simplify the DISPLAY variable even further by omitting the hostname. This feature is more than just cosmetic: with a null hostname, the client libraries use a UNIX domain socket instead of a network socket to contact the X server. In addition to being faster and more efficient, this connection method bypasses any firewall restrictions on the local system that are trying to keep out external X connections. The simplest possible value for the DISPLAY environment variable, then, is simply ":0".

## Client authentication

Although the X environment is generally thought to be relatively insecure, every precaution helps prevent unauthorized access. In the days before security was such a pressing concern, it was common for X servers to welcome connections from any client running on a host that had been marked as safe with the xhost command. But since any user on that host could then connect to your display and wreak havoc (either intentionally or out of confusion), the xhost method of granting access to clients was eventually deprecated. We do not discuss it further.

The most prevalent alternative to host-based security is called magic cookie authentication. While the thought of magic cookies might inspire flashbacks in some of our readers, in this context they are used to authenticate X connections. The basic idea is that the X display manager generates a large random number, called a cookie, early in the login procedure. The cookie for the server is written to the ~/.Xauthority file in the user's home directory. Any clients that know the cookie are allowed to connect. Users can run the xauth command to view existing cookies and to add new ones to this file.

The simplest way to show how this works is with an example. Suppose you have set your DISPLAY variable on the client system to display X applications on the machine at which you are sitting. However, when you run a program, you get an error that looks something like this:

```
client$ xprogram -display server:0
Xlib: connection to "server:0.0" refused by server
xprogram: unable to open display 'server:0'
```

This message tells you that the client does not have the right cookie, so the remote server refused the connection. To get the right cookie, log in to the server (which you have probably already done if you are trying to display on it) and list the server's cookies by running xauth list:

```
server$ xauth list
server0 MIT-MAGIC-COOKIE-1 f9d88df6077819ef4d788fab778dc9f
server/unix:0 MIT-MAGIC-COOKIE-1 f9d88df6077819ef4d788fab778dc9f
localhost:0 MIT-MAGIC-COOKIE-1 cb6cbf96e5c24128749feddd47f0e0779
```

Each network interface on the server has an entry. This example shows a cookie for the Ethernet, a cookie for the UNIX domain socket used for local connections, and a cookie for the localhost loopback network interface.

The easiest way to get the cookie onto the client (when not using SSH, which negotiates the cookie for you) is with good old cut-and-paste. Most terminal emulators (e.g., xterm) let you select text with the mouse and paste it into another window, usually by pressing the middle mouse button. Conveniently, the xauth add command accepts as input the same format that xauth list displays. You can add the cookie to the client like this:

```
client$ xauth add server:0  MIT-MAGIC-COOKIE-1
9d88df6077819e4d788fab778dc9f
```

You should verify that the cookie was added properly by running xauth list on the client. With the DISPLAY environment variable set and the correct magic cookie added to the client, applications should now display correctly on the server.

If you are having trouble getting cookies to work, you can drop back temporarily to xhost authentication just to verify that there are no other problems (for example, firewalls or local network restrictions that are preventing the client from accessing the server). Always run xhost - (that is, xhost with a dash as its only argument) to disable xhost authentication once your test is complete.

## X connection forwarding with SSH

Magic cookies increase security, but they're hardly foolproof. Any user who can obtain your display's cookie can connect to the display and run programs that monitor your activities. Even without your cookie, the X protocol transfers data over the network without encryption, allowing it to be sniffed by virtually anyone.

You can boost security with SSH, the secure shell protocol. SSH provides an authenticated and encrypted terminal service. However, SSH can also forward arbitrary network data, including X protocol data, over a secure channel. X forwarding is similar to generic SSH port forwarding, but because SSH is X-aware, you gain some additional features, including a pseudo-display on the remote machine and the negotiated transfer of magic cookies.

You typically ssh from the machine running the X server to the machine on which you want to run X programs. This arrangement can be confusing to read about because the SSH client is run on the same machine as the X server, and it connects to an SSH server that is on the same machine as the X client applications. To make it worse, the virtual display that SSH creates for your X server is local to the remote system. Exhibit B on the next page shows how X traffic flows through the SSH connection.

See page 926 for more information about SSH.
