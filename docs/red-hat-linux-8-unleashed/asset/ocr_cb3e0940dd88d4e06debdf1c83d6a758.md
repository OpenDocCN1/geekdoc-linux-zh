# CHAPTER 18 Secure File Transfer Protocol (FTP) Service

![](bbox=[0.198, 0.075, 0.792, 0.335])

FIGURE 18.2 A typical gFTP session.

After all files are uploaded or downloaded, you must close the session. Do this by clicking the red button on the top right of the application window to issue the quit command. gFTP displays the session summary information in the log panel at the bottom of the application.

Although using a graphical interface, you still need to understand the basic functionality of FTP to use gFTP. Not knowing the file type that needs to be set can result in time downloading a binary file in ASCII format, thus rendering the file unusable. gFTP defaults to a binary file type, but detects the file type during the transfer. gFTP is a robust application, providing all the necessary actions typical of an FTP session, in a pretty, easy-to-use format.

# Configuring GNOME's galleon Browser

GNOME's galleon Web browser is capable of handling a number of networking and file protocols, including FTP. The first time you launch this browser you're asked to configure various settings, such as the appearance of its toolbar, or which protocols you want galleon to handle (see Figure 18.3).

After enabling gFTP and launching the client, you can use the ftp:// URL form to access remote servers. Settings are saved in a directory named .galeon in your home directory.