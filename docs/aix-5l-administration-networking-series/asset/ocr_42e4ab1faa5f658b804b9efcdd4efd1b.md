# Account Configuration

Continue to configure the machines to allow DCE authentication logins by synchronizing the DCE registry with the local AIX user database using the following commands:

```
# dce_login cell_admin ←————You must log in as your defined administrator
# klist | grep Principal ←——Check to see if you are really cell_admin
# passwd_import ←————Answer "no" to all the questions
```

Users with no user or group identification conflicts now have DCE registry accounts. You may list, examine, enable, and set the password for these accounts with the following command line and interactive dcecp commands:

```
# dcecp -c account catalog ←———Lists all the accounts
# dcecp -c account show UserName ←——Lists the details of an account
# dcecp ←——————Starts the interactive mode needed to modify accounts
dcecp> account modify UserName -actvalid yes ←———Enables an account
dcecp> account modify UserName -password T3mP ←———Sets temporary password
```

At this point, any user on the system should be able to acquire Kerberos authentication as the new UserName principal with the following commands:

```
# dce_login UserName ←——This authenticates you
# klist ←————This will display your Kerberos ticket information
```

This may be all the authentication your applications need, but the rest of this section describes how to configure the system to allow a user to telnet in and acquire the authentication from one AIX/DCE login process. The most common need for this is to access a Distributed File Service. Other applications for this single login process are beyond the scope of this chapter.

Start the dceunixd daemon at boot time from /etc/inittab after DCE services have started. This must run on servers or clients that will allow a single AIX/DCE login (telnet, rexe, and rlogin). Otherwise, the users will have to use dce_login to acquire their authentication tickets. The following mkinitab command will add dceunixd to the /etc/inittab file:

```
# mkinitab -i rcdev \
*dceunixd:2:respawn:/bin/dceunixd -l 60 -d 1 >/dev/console 2>&1*
```

The dceunixd daemon must be started without DCE context, so the easiest way to start it is to reboot the system at this point.

Starting with AIX 4.3.3, the following DCE authentication method is included in the /usr/lib/security/methods.cfg file and the auth_method stanza in