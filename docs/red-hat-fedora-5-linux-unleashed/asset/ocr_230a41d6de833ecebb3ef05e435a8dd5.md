+   - Altering permissions users are allowed to have on the directory
+   - Limiting the time of day during which the directory is accessible

The possibilities are almost endless. Any parameters set in the individual sections override the parameters set in the `[global]` section. The following section adds a few restrictions to the `[programs]` section:

```
[programs]
path = /usr/local/programs
writable = true
valid users = ahudsonahudson
browsable = yes
create mode = 0700
```

The valid users entry limits userid to just ahudson. All other users can browse the directory because of the browsable = yes entry, but only ahudson can write to the directory. Any files created by ahudson in the directory give ahudson full permissions, but no one else will have access to the file. This is exactly the same as setting permissions with the chmod command. Again, there are numerous options, so you can be as creative as you want to when developing sections.

# Setting Global Samba Behavior with the `[global]` Section

The `[global]` section set parameters establishes configuration settings for all of Samba. If a given parameter is not specifically set in another section, Samba uses the default setting in the `[global]` section. The `[global]` section also sets the general security configuration for Samba. The `[global]` section is the only section that does not require the name in brackets.

Samba assumes that anything before the first bracketed section not labeled `[global]` is part of the global configuration. (Using bracketed headings in /etc/samba/smb.conf makes your configuration file more readable.) The following sections discuss common Samba settings to share directories and printers. You will then see how to test your Samba configuration.

# Sharing Home Directories Using the `[homes]` Section

The `[homes]` section shares out Fedora home directories for the users. The home directory is shared automatically when a user's Windows computer connects to the Linux server holding the home directory. The one problem with using the default configuration is that the user sees all the configuration files (such as .profile and others with a leading period in the filename) that he normally wouldn't see when logging on through Linux. One quick way to avoid this is to include a path option in the `[homes]` section. To use this solution, each user who requires a Samba share of his home directory needs a separate "home directory" to act as his Windows home directory.

For example, this pseudo home directory could be a directory named share in each user's home directory on your Fedora system. You can specify the path option when using