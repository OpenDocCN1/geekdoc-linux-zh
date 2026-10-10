authentication status of the connection to the server (NDS, Bindery, or none). If you connected using Bindery authentication, the username under which you're logged in on that server is also displayed. Finally, the connection numbers for each connection are displayed along with similar connection information for each bindery server that you connected to that isn't part of a NDS tree.

Because of the grace login feature of NetWare servers, even after your password expires, you are still allowed to log in a set number of times. This is to allow adequate time to make the change. Because you may be connected to many different NDS trees and NetWare servers, you must specify for which connection you want to change the password. To view your current connections and their properties, use the **nwwoami** command as explained earlier. To change the password for a NDS tree, use the **nwpasswd** command with the following syntax:

```
`nwpasswd -t tree -u username`
```

You use the same command to change the password for a bindery-based server but alter the syntax slightly:

```
`nwpasswd -s server -u username`
```

Even after your password expires, NetWare's grace login feature allows you to log in a set number of times, providing adequate time to make the password change. You might be connected to many different NDS trees and NetWare servers, so you must specify which connection the password change affects. View your current connections and their properties with the **nwwoami** command as explained earlier.

If you are changing a user's password other than your own, and you are not logged in with administrative or equivalent privileges, you will be prompted for the current password. In which case you enter the current password, then enter the new password, and finally re-enter it to confirm.

# # Printing with the NetWare Client

The NetWare client allows you to print directly to a NetWare print server and also lets you specify how those files should be printed. When you print files in NetWare, they are sent to a print queue. The print queue is a holding area where files from many users are stored; there they wait for their turn to be printed. These files are sometimes also referred to as print jobs. Using the NetWare client, you can print from the command line, and even specify how the file will print. Such options could be the number of copies, and whether or not to automatically insert carriage returns. You use the **npr1nt** command to print the specified file(s) on a specific NetWare print queue. The user must already be authenticated to the server or tree associated with the print queue. The server and queue.