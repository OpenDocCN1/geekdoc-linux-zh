+   6. Type "vi /etc/smbusers" or substitute the path and file you changed this to in Step 4. If you did change the file, copy /etc/smbusers to the new location, because a file is there already with the following contents:

```
# Unix_name = SMB_name1 SMB_name2 ...
root = administrator admin
nobody = guest pcguest smbguest
```

+   7. Each entry in this file is in the following format:

```
localuser = remote1 remote2 @localgroup ...
```

The remote1 and remote2 entries represent the usernames that people are trying to log in to the Samba server with. You can, of course, use as many or as few of these as you need. When you use the format @localgroup, you are referring to a group that already exists on the Samba server, all of whose members will log in to the service as localuser. Edit the existing lines, if you want to, and then add more users to suit your needs. For example:

```
smbusers = @users
projects = @ProjectA @ProjectB @ProjectC
```

+   8. When you are finished, press the Esc key to return to Command mode, and then type "ZZ" to save and close the file.

+   9. Restart the Samba server by typing "etc/rc.d/init.d/smb restart".

# ## Creating A Host Map

If you want to set up a host map for your site, do the following:

+   1. Log in as root to the Samba server machine you want to set up.

+   2. Type "vi /etc/smb.conf" to open the Samba server's configuration file.

+   3. Type "name resolve" and press Enter to search down for the name resolve order statement. Unedited, this statement looks like the following:

```
: name resolve order = wins lmhostos broadcast
```

+   4. Make sure that this line is uncommented—delete the semicolon—and that it is configured the way you want it, as covered in the section "Configuring Samba," earlier in the chapter.