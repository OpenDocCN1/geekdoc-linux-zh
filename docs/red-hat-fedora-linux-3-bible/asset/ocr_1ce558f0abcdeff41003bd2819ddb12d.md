# ## Using AppleTalk (netatalk) from Mac OS X

AppleTalk is the traditional set of protocols used by Apple computers to share files and printers over a LAN. Although Mac OS X can support Samba file sharing, AppleTalk is still a familiar way for Mac users to get to networked printers and files.

Inside Fedora is a software package called netatalk that you can use to configure Fedora as an AppleTalk file and printer server. To a Mac client, the netatalk server looks no different than any other AppleTalk server.

> **CROSS-REFERENCE:** Refer to the “Setting up the netatalk server” section later in this chapter.

To access a shared directory from an AppleTalk server, click Go in the Finder bar at the top of the screen, and then select Connect to Server. The Connect to Server window appears, as shown in Figure 26-2.

![](bbox=[0.09, 0.46, 0.75, 0.72])

Figure 26-2: In Mac OS X, see Samba and AppleTalk shares from the Connect to Server window.

Enter the address, as shown in Figure 26-2, or click the Browse button to see a list of available servers.

After you click Connect, a pop-up window appears, prompting for a user name and password. Use the Options window to set up your preferences for logging on to the server. You can have the password added to your keychain so you don't have to type it in each time you access the server. You can also select to send the password in clear text (which is the default) and be warned that you are doing that. The server determines whether you need to enter a clear-text or encrypted password (so if you send the wrong type of password, it will fail). You can also request a secure connection over SSH for your login (which is a good idea to prevent someone from snifffing out your password from the network).

Figure 26-3 shows the Options window for selecting password options as just described.