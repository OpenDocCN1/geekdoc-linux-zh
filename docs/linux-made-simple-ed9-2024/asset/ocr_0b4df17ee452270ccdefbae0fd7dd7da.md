# Networking:
File-sharing made easy

Why should distance be a barrier? Here are all the steps to follow to get file sharing set up on your Ubuntu PC.

Sharing files between PCs on your network is a fundamental function of modern computing, and the good news is that Ubuntu makes file sharing relatively straightforward thanks to its support for the SMB (also known as Samba) sharing standard. Ubuntu also supports another standard – NFS – but that only works with other Linux machines, so for the purposes of this tutorial we re focusing on SMB file sharing, which allows you to both access shared folders and share files from your own PC with other computers – Linux, Windows and Mac – on your network.

+   **Quick tip**
+   If you’re on someone else’s computer, make sure you don’t choose the ‘remember’ option when connecting to a shared folder, otherwise anyone will be able to reconnect using your credentials.

to match a profile set up on your target computer (typically your own user profile on that computer). If you are connecting to a public folder, leave the username blank and click Connect. You’ll be asked if you want to connect anonymously – leave this selected.

Before clicking Connect, you’ll also see an option to save your user credentials so save you the bother of providing them the next time you connect – choose carefully here (see the tip box). Once connected, the shared folder works like any other: you’ll be able to easily drag files from it to your PC, and – if the folder’s shared permissions allow it – you can copy files into that folder too.

It’s simple and incredibly straightforward, but note that the path to the shared folder is lost each time you restart your PC, forcing you to manually browse to that folder again in order to connect to it. One way to save you some time when reconnecting to a frequently used shared folder is to create a bookmark to it in Files. Simply right-click the shared folder’s entry in the left-hand pane underneath the ‘Browse Network’ button and choose ‘Add Bookmark’. You’ll see the bookmark appear at the bottom of the left-hand pane, and reconnecting in future is as simple as clicking the shortcut.

![](bbox=[0.09, 0.685, 0.51, 0.92])

It’s also possible to automatically connect to shared folders when Ubuntu launches, but this involves a trip to the Terminal. A simpler alternative involves installing an app called Gigolo from the Software Centre. Once installed, open it from its shortcut icon in the launcher.

Gigolo allows you to browse, connect and bookmark shared folders with ease – the annotation reveals how it works in more detail. As things stand, you’ll need to launch Gigolo after starting Ubuntu to automatically connect to those shared folders. To solve this problem, configure Gigolo to start with Ubuntu: open dash and type ‘startup’, then launch ‘Startup Applications’. Click ‘Add’. Name it ‘Gigolo’, then type /usr/bin/gigolo into the Command box. Add a suitably descriptive comment such as ‘Mount shares at startup’ and click ‘Add’.