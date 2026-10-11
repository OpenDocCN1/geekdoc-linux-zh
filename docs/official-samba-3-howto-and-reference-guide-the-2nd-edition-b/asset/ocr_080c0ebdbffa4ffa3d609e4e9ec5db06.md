+   • Create a GPO that enforces this through Active Directory, and place the new default profile in the NETLOGON share.

The registry hive key that affects the behavior of folders that are part of the default user profile are controlled by entries on Windows 2000/XP is:

```
HKEY_CURRENT USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\
```

This hive key contains a list of automatically managed folders. The default entries are shown in Table 26.3

# Table 26.3 Defaults of Default User Profile Paths Registry Keys

| Name | Default Value |
| :--- | :--- |
| AppData | %USERPROFILE%\ Application Data |
| Cache | %USERPROFILE%\Local Settings\Temporary Internet Files |
| Cookies | %USERPROFILE%\Cookies |
| Desktop | %USERPROFILE%\Desktop |
| Favorites | %USERPROFILE%\Favorites |
| History | %USERPROFILE%\Local Settings\History |
| Local AppData | %USERPROFILE%\Local Settings\Application Data |
| Local Settings | %USERPROFILE%\Local Settings |
| My Pictures | %USERPROFILE%\My Documents\My Pictures |
| NetHood | %USERPROFILE%\NetHood |
| Personal | %USERPROFILE%\My Documents |
| PrintHood | %USERPROFILE%\PrintHood |
| Programs | %USERPROFILE%\Start Menu\Programs |
| Recent | %USERPROFILE%\Recent |
| SendTo | %USERPROFILE%\SendTo |
| Start Menu | %USERPROFILE%\Start Menu |
| Startup | %USERPROFILE%\Start Menu\Programs\Startup |
| Templates | %USERPROFILE%\Templates |

There is also an entry called “Default” that has no value set. The default entry is of type REG_SZ; all the others are of type REG_EXPAND_SZ.

It makes a huge difference to the speed of bundling roaming user profiles if all the folders are stored on a dedicated location on a network server. This means that it will not be necessary to write the Outlook PST file over the network for every login and logout.

To set this to a network location, you could use the following examples:

```
%LOGONSERVER%\%USERNAME%\Default Folders
```

This stores the folders in the user’s home directory under a directory called Default Folders. You could also use: