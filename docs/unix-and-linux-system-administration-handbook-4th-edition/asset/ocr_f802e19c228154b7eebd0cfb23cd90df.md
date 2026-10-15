Each network interface on the server has an entry. This example shows a cookie for the Ethernet, a cookie for the UNIX domain socket used for local connections, and a cookie for the localhost loopback network interface.

The easiest way to get the cookie onto the client (when not using SSH, which negotiates the cookie for you) is with good old cut-and-paste. Most terminal emulators (e.g., xterm) let you select text with the mouse and paste it into another window, usually by pressing the middle mouse button. Conveniently, the xauth add command accepts as input the same format that xauth list displays. You can add the cookie to the client like this:

```
client$ xauth add server:0  MIT-MAGIC-COOKIE-1
9d88df6077819e4d788fab778dc9f
```

You should verify that the cookie was added properly by running xauth list on the client. With the DISPLAY environment variable set and the correct magic cookie added to the client, applications should now display correctly on the server.

If you are having trouble getting cookies to work, you can drop back temporarily to xhost authentication just to verify that there are no other problems (for example, firewalls or local network restrictions that are preventing the client from accessing the server). Always run xhost - (that is, xhost with a dash as its only argument) to disable xhost authentication once your test is complete.

# X connection forwarding with SSH

Magic cookies increase security, but they're hardly foolproof. Any user who can obtain your display's cookie can connect to the display and run programs that monitor your activities. Even without your cookie, the X protocol transfers data over the network without encryption, allowing it to be sniffed by virtually anyone.

You can boost security with SSH, the secure shell protocol. SSH provides an authenticated and encrypted terminal service. However, SSH can also forward arbitrary network data, including X protocol data, over a secure channel. X forwarding is similar to generic SSH port forwarding, but because SSH is X-aware, you gain some additional features, including a pseudo-display on the remote machine and the negotiated transfer of magic cookies.

You typically ssh from the machine running the X server to the machine on which you want to run X programs. This arrangement can be confusing to read about because the SSH client is run on the same machine as the X server, and it connects to an SSH server that is on the same machine as the X client applications. To make it worse, the virtual display that SSH creates for your X server is local to the remote system. Exhibit B on the next page shows how X traffic flows through the SSH connection.

See page 926 for more information about SSH.