![](bbox=[0.29, 0.11, 0.68, 0.36])

+   3. Type the user name and password. (Optionally, you can click the Add to Keychain box. The keychain lets you store your user name and password, so you don’t have to type it again the next time you access this Samba share.) An icon representing the Samba share should appear on your desktop.

If the Samba server doesn’t appear on the Connect to Server window, you can type the name or IP address of the server, followed by the share name you want in the address box on the bottom of the window. Here’s an example of an address for accessing a Samba share from the Connect to Server window:

```
smb://192.168.0.3/toyprojects
```

In this example, smb tells Mac OS X that it is looking for a Samba share. The Samba server in this example is located at IP address 192.168.0.3 (you could use a NetBIOS name instead of an IP address here). The name of the share is toyprojects. You could also add the workgroup and user name to the command line. Here’s an example that asks for a share named toyprojects on a server named toys, in the ESTREET workgroup, as the user named chris:

```
smb://ESTREET:chris@toys/toyprojects
```

Here are a few things you should know about accessing Samba shares from Mac OS X:

+   - When authenticating your password (see Figure 26-4), Mac OS X sends your password in clear text. Unlike when authenticating on an AppleTalk share, there is no way to select to send encrypted passwords from this window.

+   - The example of setting up Linux Samba shares in Chapter 18 shows how to set up Samba to ask for encrypted passwords (and therefore will fail authentication from Mac OS X). To get around the problem (on a secure network), you can create a share that either accepts clear-text passwords or have the share be available to guest users.