
## Using the gFTP Interface

The GNOME gFTP client provides all the typical features of FTP, including the ability to save profiles of common connections. Figure 23.1 shows a typical gFTP session in action. On the left panel is the local host, and on the right panel is the remote server. A connection is initiated by typing the address of the host into the host field, a specific port if not the standard FTP port (21), a valid username for the server, and a password. After the information has been entered, clicking the icon that looks like a monitor will start the connection to the server. The bottom panel displays session information, such as changing directories, as seen in Figure 23.1.

![](img/e464b828c497c99e41f61d4c55f1c0db_575_0.png)

FIGURE 23.1 A typical gFTP session.

gFTP sets the file type as binary by default, which can be changed by clicking on ASCII in the FTP drop-down menu. To upload a file to the server, the user clicks on a filename in the left panel and clicks on the right arrow icon. The file is then transferred to the server, and the right panel will be updated to reflect this new file being added to the server. Similarly, to download a file from the server, the user selects the correct file type from the drop-down menu, selects the file to be downloaded, and clicks the left arrow icon. The left panel will then be updated to show the result of the transfer, with logging information shown in the bottom panel.

After all files are uploaded or downloaded, you must close the session. Do this by clicking the red button on the top right of the application window to issue the quit command. gFTP displays the session summary information in the log panel at the bottom of the application. You can also close the session simply by exiting gFTP.

## FTP Sessions with Konqueror and Nautilus

Both KDE and GNOME file browsers have integrated FTP functionality built in. Use an ftp:// URL followed by a server name or IP address to start an anonymous FTP session. The drag-and-drop feature of KDE and the GNOME window manager allow users to select remote files and drag them to the desktop.

KDE's Konqueror web browser is capable of handling a number of networking and file transfer protocols, including FTP. You can configure various setting for this browser, such as the appearance of the browser's toolbar, but one of Konqueror's best features is its flexibility for file transfers.

Start the browser by clicking its icon on the KDE's kicker desktop panel or by typing the following at the command line:

```
$ konqueror &
```

After launching the client, you can use the ftp:// URL form to access remote servers, as shown in Figure 23.2.

![](img/e464b828c497c99e41f61d4c55f1c0db_576_0.png)

FIGURE 23.2 KDE's Konqueror web browser can access remote FTP servers using URLs.

If your window manager does not support drag and drop, you can use Konqueror's Copy Files feature to retrieve a file. First, type in an FTP URL (such as ftp://ftp.tux.org). Next, navigate to a desired directory and click to select a desired file. You then click the Edit menu's Copy Files menu item (or press F7). A Save dialog will appear, and you can select your home directory to save the file. After you press Enter, a file download progress dialog will be displayed while the file is being retrieved.

You can also use the Nautilus browser to retrieve files from a remote server.

Figure 23.3 shows an anonymous login to a remote FTP server using Nautilus. Connect to a remote FTP server using File > Connect to Server, then simply click to select a file, select Copy from the Edit menu (or press Ctrl+C), click to go to your home directory (using the icon in the Nautilus toolbar), and then click Paste (or press Ctrl+V) to retrieve and save the file.

![](img/e464b828c497c99e41f61d4c55f1c0db_577_0.png)

FIGURE 23.3 The Nautilus file browser can be used for FTP sessions through the Places > Connect to Server menu option.

These types of intuitive features can shield users from needing to know the details of how FTP works or memorizing various commands.

## FTP Servers

FTP uses a client/server model. As a client, FTP accesses a server, and as a server, FTP provides access to files or storage. Just about every computer platform available has software written to enable a computer to act as an FTP server, but Ubuntu provides the average user the ability to do this without paying hefty licensing fees and without regard for client usage limitations.

There are two types of FTP servers and access: anonymous and standard. A standard FTP server requires an account name and password from anyone trying to access the server. Anonymous servers allow anyone to connect to the server to retrieve files. Anonymous servers provide the most flexibility, but they can also present a security risk. Fortunately, as you will read in this chapter, Ubuntu is set up to use proper file and directory permissions and commonsense default configuration, such as disallowing root to perform an FTP login.
