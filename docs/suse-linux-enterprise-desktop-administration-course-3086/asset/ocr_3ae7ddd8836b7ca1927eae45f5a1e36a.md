If no location is specified, the symbolic link is created in the Map Link Default Location configured in the System Settings or in your home directory.

3. Type the name of the symbolic link to be created, or select a letter from the drop-down list (if you want to use a single letter as the name for the link).

4. In the Novell File System field, type the server name and the path to the directory you want to map.

The path can be in any of the following forms:

```
//server/volume/path
server/volume:
server/volume:/path
or
.directory_
object_name.fully_distinguished_eDirectory_path
```

(such as a cluster volume, for example: my_dir.users.acct.mycompany)
You can also select the Browse button and locate the directory you want to map.

5. (Optional) To reestablish this drive mapping the next time you log in, select Map this drive at startup.

6. Select Map.

The mapped drive appears in your home directory (by default) or in the directory you specified in Step 2.

# Disconnecting a Mapped Directory

+   1. Select >Disconnect Novell Mapped Directory.
+   2. Select the mapped directory that you want to disconnect from; then select Disconnect.

# Editing Your Login Script
This option lets you edit or create the personal login script that runs when you log in.
Check with your network administrator before creating or changing a login script. Your network administrator can tell you if you should create a personal login script on your network and can provide information on script syntax.
1. Select > User Administration for Name_of_Tree > Edit Login Script.