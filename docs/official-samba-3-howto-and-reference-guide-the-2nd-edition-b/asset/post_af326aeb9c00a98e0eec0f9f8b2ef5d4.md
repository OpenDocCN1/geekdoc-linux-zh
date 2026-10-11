
HKEY_CURRENT_USER
\Software
\Microsoft
\Windows
\CurrentVersion
\Explorer
\User Shell Folders

The above hive key contains a list of automatically managed folders. The default entries are shown in Table 26.1.

### Table 26.1 User Shell Folder Registry Keys Default Values

| Name | Default Value |
|:---|:---|
| AppData | %USERPROFILE%\Application Data |
| Desktop | %USERPROFILE%\Desktop |
| Favorites | %USERPROFILE%\Favorites |
| NetHood | %USERPROFILE%\NetHood |
| PrintHood | %USERPROFILE%\PrintHood |
| Programs | %USERPROFILE%\Start Menu\Programs |
| Recent | %USERPROFILE%\Recent |
| SendTo | %USERPROFILE%\SendTo |
| Start Menu | %USERPROFILE%\Start Menu |
| Startup | %USERPROFILE%\Start Menu\Programs\Startup |

The registry key that contains the location of the default profile settings is:

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders

The default entries are shown in Table 26.2.

### Table 26.2 Defaults of Profile Settings Registry Keys

| Name | Default Value |
|:---|:---|
| Common Desktop | %SystemRoot%\Profiles\All Users\Desktop |
| Common Programs | %SystemRoot%\Profiles\All Users\Programs |
| Common Start Menu | %SystemRoot%\Profiles\All Users\Start Menu |
| Common Startup | %SystemRoot%\Profiles\All Users\Start Menu\Programs\Startup |

### 26.5.3 MS Windows 200x/XP

> **NOTE**
>
> MS Windows XP Home Edition does use default per-user profiles, but cannot participate in domain security, cannot log onto an NT/ADS-style domain, and thus can obtain the profile only from itself. While there are benefits in doing this, the beauty of those MS Windows clients that can participate in domain logon processes is that they allow the administrator to create a global default profile and enforce it through the use of Group Policy Objects (GPOs).

When a new user first logs onto an MS Windows 200x/XP machine, the default profile is obtained from C:\Documents and Settings\Default User. The administrator can modify or change the contents of this location, and MS Windows 200x/XP will gladly use it. This is far from the optimum arrangement, since it will involve copying a new default profile to every MS Windows 200x/XP client workstation.

When MS Windows 200x/XP participates in a domain security context, and if the default user profile is not found, then the client will search for a default profile in the NETLOGON share of the authenticating server. In MS Windows parlance, it is \\LOGON-SERVER\\NETLOGON\\Default User, and if one exists there, it will copy this to the workstation in the C:\Documents and Settings\ under the Windows login name of the user.

> **NOTE**
>
> This path translates, in Samba parlance, to the smb.conf [NETLOGON] share. The directory should be created at the root of this share and must be called Default User.

If a default profile does not exist in this location, then MS Windows 200x/XP will use the local default profile.

On logging out, the user’s desktop profile is stored to the location specified in the registry settings that pertain to the user. If no specific policies have been created or passed to the client during the login process (as Samba does automatically), then the user’s profile is written to the local machine only under the path C:\Documents and Settings\USERNAME\.

Those wishing to modify the default behavior can do so through these three methods:

- Modify the registry keys on the local machine manually and place the new default profile in the NETLOGON share root. This is not recommended because it is maintenance intensive.
- Create an NT4-style NTConfig.POL file that specifies this behavior and locate this file in the root of the NETLOGON share along with the new default profile.
- Create a GPO that enforces this through Active Directory, and place the new default profile in the NETLOGON share.

The registry hive key that affects the behavior of folders that are part of the default user profile are controlled by entries on Windows 2000/XP is:

```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\
```

This hive key contains a list of automatically managed folders. The default entries are shown in Table 26.3.

### Table 26.3 Defaults of Default User Profile Paths Registry Keys

| Name | Default Value |
| :--- | :--- |
| AppData | %USERPROFILE%\Application Data |
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

```
\\SambaServer\FolderShare\%USERNAME\
```

in which case the default folders are stored in the server named SambaServer in the share called FolderShare under a directory that has the name of the MS Windows user as seen by the Linux/UNIX file system.

Please note that once you have created a default profile share, you must migrate a user's profile (default or custom) to it.

MS Windows 200x/XP profiles may be local or roaming. A roaming profile is cached locally unless the following registry key is created:

```
HKEY_LOCAL_MACHINE\SYSTEM\Software\Microsoft\Windows NT\CurrentVersion\winlogon\"DeleteRoamingCache"=dword:00000001
```

In this case, the local cache copy is deleted on logout.

## 26.6 Common Errors

The following are some typical errors, problems, and questions that have been asked on the Samba mailing lists.

### 26.6.1 Configuring Roaming Profiles for a Few Users or Groups

With Samba-2.2.x, the choice you have is to enable or disable roaming profiles support. It is a global-only setting. The default is to have roaming profiles, and the default path will locate them in the user's home directory.

If disabled globally, then no one will have roaming profile ability. If enabled and you want it to apply only to certain machines, then on those machines on which roaming profile support is not wanted, it is necessary to disable roaming profile handling in the registry of each such machine.

With Samba-3, you can have a global profile setting in smb.conf, and you can override this by per-user settings using the Domain User Manager (as with MS Windows NT4/200x).

In any case, you can configure only one profile per user. That profile can be either:

- A profile unique to that user.
- A mandatory profile (one the user cannot change).
- A group profile (really should be mandatory --- that is, unchangeable).

### 26.6.2 Cannot Use Roaming Profiles

A user requested the following: “I do not want roaming profiles to be implemented. I want to give users a local profile alone. I am totally lost with this error. For the past two days I tried everything, I googled around but found no useful pointers. Please help me.”

The choices are:

- **Local profiles**: I know of no registry keys that will allow autodetection of LOCAL profiles on log out.
- **Roaming profiles**: As a user logs onto the network, a centrally stored profile is copied to the workstation to form a local profile. This local profile will persist (remain on the workstation disk) unless a registry key is changed that will cause this profile to be automatically deleted on logout.

The roaming profile choices are:

- **Personal roaming profiles**: These are typically stored in a profile share on a central (or conveniently located local) server.
    - Workstations cache (store) a local copy of the profile. This cached copy is used when the profile cannot be downloaded at next logon.
- **Group profiles**: These are loaded from a central profile server.
- **Mandatory profiles**: Mandatory profiles can be created for a user as well as for any group that a user is a member of. Mandatory profiles cannot be changed by ordinary users. Only the administrator can change or reconfigure a mandatory profile.

A Windows NT4/200x/XP profile can vary in size from 130KB to very large. Outlook PST files are most often part of the profile and can be many gigabytes in size. On average (in a well controlled environment), roaming profile size of 2MB is a good rule of thumb to use for planning purposes. In an undisciplined environment, I have seen up to 2GB profiles. Users tend to complain when it takes an hour to log onto a workstation, but they harvest the fruits of folly (and ignorance).

The point of this discussion is to show that roaming profiles and good controls of how they can be changed as well as good discipline make for a problem-free site.

Microsoft's answer to the PST problem is to store all email in an MS Exchange Server backend. This removes the need for a PST file.

Local profiles mean:

- If each machine is used by many users, then much local disk storage is needed for local profiles.
- Every workstation the user logs into has its own profile; these can be very different from machine to machine.

On the other hand, use of roaming profiles means:

- The network administrator can control the desktop environment of all users.
- Use of mandatory profiles drastically reduces network management overheads.
