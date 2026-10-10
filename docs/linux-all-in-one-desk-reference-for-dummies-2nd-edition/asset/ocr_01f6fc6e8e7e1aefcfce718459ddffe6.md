# # Chapter 4: Using FTP

+   - **In This Chapter**  
+   - Using the GNOME FTP client  
+   - Using any Web browser as an FTP client  
+   - Getting to know the FTP commands

Just as the name implies, *File Transfer Protocol* (FTP) is used to transfer files between computers. For example, if your Internet Service Provider (ISP) gives you space for a personal Web site, you may have already used FTP to upload the files making up the Web site. Using an FTP client on your computer, you log in to your ISP account, provide your password, and then copy the files from your home system to the ISP's server.

You can also use FTP to download other files anonymously, such as open source software from other computers on the Internet — in which case, you don't need an account on the remote system to download files. You can simply log in using the word *anonymous* as the username and provide your e-mail address as the password. (In fact, your Web browser can do this on your behalf, so you may not even know this process is happening.) This type of anonymous FTP is great for distributing files to anyone who wants them. For example, a hardware vendor might use anonymous FTP to provide updated device drivers to anyone who needs them.

Linux comes with several FTP clients, both command-line ones and GUI ones. In this chapter, I introduce you to a few GUI FTP clients and for the command-line FTP client, describe the commands you use to work with remote directories.

# ## Using Graphical FTP Clients

You can use one of the following GUI FTP clients in Linux:

+   - gFTP — a graphical FTP client for GNOME ([http://gftp.seul.org](http://gftp.seul.org))  
+   - KBear — a graphical FTP client for KDE ([http://kbear.sourceforge.net](http://kbear.sourceforge.net))  
+   - Web browser, such as Firefox, for anonymous FTP downloads