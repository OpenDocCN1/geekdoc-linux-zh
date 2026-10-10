can change the anonymous user or group, respectively. For example, \textit{anonuid}=175 sets all anonymous users to UID 175 and \textit{anongid}=300 sets the GID to 300. (Only the number is displayed when you list file permission, however, unless you add entries with names to \textit{/etc/passwd} and \textit{/etc/group} for the new UIDs and GIDs.)

+   • \textbf{User mapping} — If the same users have login accounts for a set of computers (and they have the same IDs), NFS, by default, will map those IDs. This means that if the user named mike (UID 110) on maple has an account on pine (mike, UID 110), he could use his own remotely mounted files from either computer.

If a client user who is not set up on the server creates a file on the mounted NFS directory, the file is assigned to the client’s UID and GID. (An \textit{ls -ln} on the server would show the UID of the owner.)

# Exporting the shared file systems

After you have added entries to your \textit{/etc/exports} file, you can actually export the directories listed using the \textit{exportfs} command. If you reboot your computer or restart the NFS service, the \textit{exportfs} command is run automatically to export your directories. However, if you want to export them immediately, you can do so by running \textit{exportfs} from the command line (as root).

> **TIP:** It’s a good idea to run the \textit{exportfs} command after you change the \textit{exports} file. If any errors are in the file, \textit{exportfs} will identify those errors for you. If you are not able to immediately access changed NFS shares from clients, you might need to restart the NFS and portmap services.

Here’s an example of the \textit{exportfs} command:

```
# "/usr/sbin/exportfs -a -r -v"
exporting maple:/public
exporting spruce:/public
exporting maple:/home
exporting spruce:/home
exporting */:mnt/win
```

The \textit{-a} option indicates that all directories listed in \textit{/etc/exports} should be exported. The \textit{-r} option will cause any previously existing exports to pick up new options. The \textit{-v} option says to print verbose output. In this example, the \textit{/public} and \textit{/home} directories from the local server are immediately available for mounting by those client computers that are named (maple and spruce). The \textit{/mnt/win} directory is available to all client computers.

Running the \textit{exportfs} command makes your exported NFS directories immediately available. Any changes to your \textit{/etc/export} file will be used again the next time you reboot or otherwise restart the NFS service.