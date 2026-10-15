# Using the gFTP Interface

The GNOME gFTP client provides all the typical features of FTP, including the ability to save profiles of common connections. Figure 23.1 shows a typical gFTP session in action. On the left panel is the local host, and on the right panel is the remote server. A connection is initiated by typing the address of the host into the host field, a specific port if not the standard FTP port (21), a valid username for the server, and a password. After the information has been entered, clicking the icon that looks like a monitor will start the connection to the server. The bottom panel displays session information, such as changing directories, as seen in Figure 23.1.

![](bbox=[0.11, 0.35, 0.65, 0.8])

FIGURE 23.1 A typical gFTP session.

gFTP sets the file type as binary by default, which can be changed by clicking on ASCII in the FTP drop-down menu. To upload a file to the server, the user clicks on a filename in the left panel and clicks on the right arrow icon. The file is then transferred to the server, and the right panel will be updated to reflect this new file being added to the server. Similarly, to download a file from the server, the user selects the correct file type from the drop-down menu, selects the file to be downloaded, and clicks the left arrow icon. The left panel will then be updated to show the result of the transfer, with logging information shown in the bottom panel.

After all files are uploaded or downloaded, you must close the session. Do this by clicking the red button on the top right of the application window to issue the quit command. gFTP displays the session summary information in the log panel at the bottom of the application. You can also close the session simply by exiting gFTP.