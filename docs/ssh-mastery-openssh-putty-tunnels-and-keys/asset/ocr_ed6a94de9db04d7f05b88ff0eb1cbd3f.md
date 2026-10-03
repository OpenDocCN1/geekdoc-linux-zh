puttygen, if you didn’t install those as part of PuTTY. We’ll use those in Chapter 7.

Start WinSCP and you’ll see this screen.

![](bbox=[0.148, 0.15, 0.883, 0.535])

Figure 6-1: WinSCP Login

The left side contains your saved connections. Set up new connections on the right. Enter the server’s hostname, your username, and your password. Change the port if needed. You can save this connection by hitting Save.

WinSCP can import your PuTTY host key cache. Select Tools->Import. You’ll see the contents of PuTTY’s key cache, with a check box by each. Verify every server you want to use is checked, then select OK. WinSCP can now piggyback on all the work you did verifying host keys.

Once you verify a host key in PuTTY, you can go back into WinSCP and import the verified key there.

# Using WinSCP

Double-click on WinSCP. Enter your username, password, and the hostname of your SSH server. WinSCP will log in and open a double window. The left side shows your local home directory, while the right side shows your home directory on the remote server. This is called a “Commander-Style” interface. Drag and drop files from one side to the other.

You can tell WinSCP to use an “Explorer-style” interface. It will open a