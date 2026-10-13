+   - **When you change a user’s shell to a newly installed shell you are warned that the shell is not valid:** This occurs because the `/etc/shells` file must contain a list of valid shells. Add the new shell to the end of the list in this file.
+   - **After installing the shadow password suite, system services such as FTPD, IMAP, and Samba no longer allow users to log in:** This occurs because the Shadow Password Suite changes the password verification program and these applications must be rebuilt to support shadow passwords. Consult the Shadow Password HOWTO at `http://www.linuxdoc.org/HOWTO/Shadow-Password-HOWTO.html` for more details.

# USEFUL SCRIPTS

If you perform much user management, you should consider creating scripts to automate some of the more common processes. In this section we present two scripts as examples of user management scripts you might want to create for your system:

+   - `disableuser`
+   - `enableuser`

# disableuser

As discussed earlier in the “Disabling Users” section, you can disable a user by changing their shell to a tail script. The following script, `disableuser`, disables users in this way assuming you have a tail script with an appropriate message at `/usr/local/bin/disabled` as outlined in the “Disabling Users” section.

The following is the source code for the script:

```
```sh
#!/bin/sh

/usr/bin/chsh -s /usr/local/bin/disabled $1
echo User $1 is disabled.
```
```

Create this script as the file `/usr/local/bin/disableuser` and make it executable:

```
```sh
# chmod o+x /usr/local/bin/disableuser
```
```

You can disable users with the script as follows:

```
```sh
# disableuser <username>
```
```

# enableuser

As discussed earlier in the “Disabling Users” section, you can disable a user by changing their shell to a tail script. The following script, `enableruser`, enables users that have been disabled in this way.