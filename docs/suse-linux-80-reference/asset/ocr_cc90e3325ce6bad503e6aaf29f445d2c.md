Along with `AppleVolumes.default`, additional files can be created, such as `AppleVolumes.guest`, used by some servers (by giving the option `-defaultvol` in the `afpd.conf` file — see previous section). The syntax

```
/usr/local/psfonts "PostScript Fonts"
```

indicates that the Linux directory `/usr/local/psfonts` located in the root directory is available as an AppleShare volume with the name "PostScript Fonts". Options are separated by a space and attached to the end of a line. A very useful option is the access restriction:

```
/usr/local/psfonts "PostScript Fonts" allow:User1,@group0
```

which restricts access to the volume "PostScript Fonts" to the user "User1" and all members of the group "group0". The users and groups entered here have to be known, of course, to the Linux system. Likewise, explicitly deny users access with `deny:User2`.

These restrictions only apply to access via AppleTalk and not to the normal access rights users have if they can log in to the server itself.

Netatalk maps the customary Resource Fork of MacOS files to `.AppleDouble` directories in the Linux file system. Using the `nodouble` option, set these directories to be created only when they are actually needed. Syntax:

```
/usr/local/guests "Guests" options:nodouble
```

Additional options and features can be found in the explanations included in the file itself.

The tilde (`~`) in this configuration file stands for the home directory for each and every user on the server. This way, every user can easily access his home directory without each one having to be explicitly defined here. The example file installed already includes a tilde, which is why Netatalk makes the home directory available by default as long as you do not modify anything in this file.

`afpd` also searches for a file `AppleVolumes` or `.AppleVolumes` in the home directory of a user logged on to the system. Entries in this file supplement the entries in the server files `AppleVolumes.system` and `AppleVolumes.default` to enable individual type and creator file specifications and to access specific directories. These entries are extensions and do not allow access for the user for whom access permission is denied from the server side.

The `netatalk.pam` file is used, via PAM (pluggable authentication modules), for authentication purposes. Using PAM is, however, irrelevant in this context.