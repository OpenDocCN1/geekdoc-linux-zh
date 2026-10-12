# Sharing netatalk volumes

You use the AppleVolumes.default file to indicate which volumes from the netatalk server are made available to your Mac clients. This file is located in /etc/atak/AppleVolumes.default.

> NOTE: See "File/directory-level security" for detailed information on hidden files and directories, as well as user/group permissions issues related to sharing volumes.

Look at the last line in the AppleVolumes.default file. The single tilde (~) on a line by itself tells the AppleTalk daemon to make all Linux home directories (usually in the /home directory) available as AppleTalk shared directories. When a user logs into the netatalk server, the user’s own home directory appears as an available shared directory. A user that chooses to open that directory has the same rights to change, add, and delete files that he has when logged in directly to Linux.

A common practice is to add the text “Home Directory” to the line that contains the single tilde (~) so that it appears as follows:

```
~ "Home Directory"
```

Sharing additional directories can be done by simply adding a full path name to the directory you want to share and the volume name you want to assign to it. For example:

```
/var/toyprojects "Linux Toys"
```

As you can see in this example, /var/toyprojects is shared under the name "Linux Toys". The path name is limited to 27 characters. In this simple case, access permissions to the volume are determined by the user, host, and folder-level security that is set up for the volume (see the "Securing netatalk volumes" section for more information).

You can also add options directly to each listing in the AppleVolumes.default file. On the same line, after the path (/var/toyprojects) and volume name ("Linux Toys") options as shown above, you can add some options. Here are a few options that might interest you (look inside the AppleVolumes.default file for others):

+   * casefold:option — Normally, when a shared volume appears on the Mac client’s screen, file and directory names appear in upper- and lowercase as they exist on the Linux system. By replacing option in the casefold option with tolower or toupper, you can have lowercase or uppercase appear in both directions, respectively. Or, you could have case translated (xlatelower or xlaterupper) to set what the client sees.
+   * allow:users/@groups or deny:users/@groups — You could add specific users or groups to an allow or deny option to have those users or groups allowed or denied access to the shared volume. (Separate each with a comma; indicate a group with an @ sign.)