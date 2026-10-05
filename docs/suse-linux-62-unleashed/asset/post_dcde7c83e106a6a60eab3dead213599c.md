
Transferring rpc.bynumber...
Trying ypxfrd ... not running
[etc...]

denon.domain.com's NIS database has been set up.
If there were warnings, please figure out what went wrong, and fix it.

At this point, make sure that /etc/passwd and /etc/group have been edited so that the NIS is activated, the databases you have just created will be used, instead of the /etc ASCII files.

Don't worry about the Trying ypxfrd... not running message. In fact, I have set the NIS master server to run the YP map transfer rpc.ypxfrd. In fact, I never set it up to do so; use a server push method that the NIS master server pushes the maps to all the NIS slaves whenever there is an update.

To set the NIS master for the actual task, you need to change its makefile a little. On the server, edit the makefile so that the line NOPUSH="True" is changed to read #NOPUSH="True" and the line that reads DOMAIN = 'basename \pwd\' is changed to DOMAIN='/bin/domainname'.

For the big test: On the NIS master server, run cd /var/yp;make all to force all the maps to be rebuilt and pushed. The output should look something like this:

+   Updating passwd.byname....
Pushed passwd.byname map.
Updating passwd.byuid....
Pushed passwd.byuid map.
Updating hosts.byname....
Pushed hosts.byname.
Updating hosts.byaddr....
Pushed hosts.byaddr.
[etc...]

On the NIS slave server, change the /etc/yp.conf file so that the ypserver is set to point to the server. Run the command ypcat passwd and see whether your NIS password file is displayed. If so, you're set. The NIS slave server is configured.

If you're having problems, trace through your steps. Also be to reboot the machine and see if your NIS slave server still works correctly. If it doesn't come back up, be sure that the changes you made to the boot sequence when installing ypserv were correct.

# NIS
CHAPTER 14 461

# Tip

If your NIS client or slave server seems to have a hard time finding other hosts on the network, be sure that the /etc/nsswitch.conf file is set to resolve hosts by file before NIS. Be sure that all the important hosts needed for the NIS servers to set themselves up in their own local /etc/hosts file.

## Using NISisms in Your /etc/passwd File

The most popular use of NIS is to keep a global user database so that it is possible to grant access to any machine at your site to any user. Under SuSE Linux, this behavior is implicit for all NIS clients.

Sometimes, you do not want everyone accessing certain systems, such as those used by personnel. You can fix this by using the special token + in your /etc/passwd file. By default, NIS clients have the line +:::::: at the end of their /etc/passwd file, allowing everyone in NIS to log in to the system. To arrange that the line remains an NIS client but does not grant everyone permission, change the line to read +::::::/bin/false. This will allow only people with actual entries in the /etc/passwd file for that host (for example, root) to log in.

To allow a specific person to log in a host, you can add a line to the /etc/passwd file granting this access. The format of the line is +username:::::: where username is the login of the user you want to grant access. NIS will automatically grab the user's passwd entry from the NIS server and use the correct information for determining the user information (for example, UID, GID, GECOS, and so on). You can override particular fields by inserting the new value in the +username:::::: entry. For example, if the user sshah uses /usr/local/bin/tesh as his shell, the host he needs to log in to keeps it in /bin/tesh, you can set it /etc/passwd entry to +shah::::::bin/tesh.

## Using Netgroups

Netgroups are a great way to group people and machines into nice, neat names for access control. A good example of using this feature is for a site where users are not allowed to log in server machines. You can create a netgroup for the system administrators and let members of the group through a special entry to the /etc/passwd file.

![](img/cbac72550c7126a22162e94d91a0c360_496_0.png)

# Networking and Internet Services
PART II

Netgroup information is kept in the /etc/netgroup file and shared via NIS.

The format of a netgroups file is as follows:

```
groupname member-list
```

groupname is the name of the group defined, and the member-list consists of other group names or tuples of specific data. Each entry in the member-list is separated by a whitespace.

A tuple containing specific data comes in the following form:

```
(hostname, username, domain name)
```

hostname is the name of the machine for which that entry is valid, username is the login of the person being referenced, and domain name is the NIS domain name. Any entry left blank is a wildcard; for example, (technics,,) implies everybody on the host technics. With a dash in it (-) means that there are no valid values for that entry. For example, (-,sshah) implies the user ssh and nothing else. This is useful for generating a list of users or group names for other netgroups.

In files where netgroups are supported (such as /etc/passwd), you reference them by placing an @ in front of them. If you want to give the netgroup sysadmins consisting of (-,sshah,), (-heidis,) permission to log in to a server, you add the following line to your /etc/passwd file:

```
+@sysadmins
```

An example of a full netgroups file follows:

+   sysadmins (-,sshah,), (-heidis,), (-nguyen,), (-mpham,)
servers (numark,-), (vestax,-)
clients (denon,-), (technics,-) mtx,-)
research-1 (-boson,-), (-jyom,-), (-weals,-), (-jaffe,-)
research-2 (-sangeet,-), (-mona,-), (-paresh,-), (-marjani,-), (-jagdish,-)
consultants (-arturo,-)
allusers sysadmins research-1 research-2 consultants
hosts servers clients

As a general rule, the line lengths should be no more than 1024. Although the system has no problems with the greater line, it is difficult to edit the file.

# Some Troubleshooting Tips

The NIS software isn’t behaving as you think it should, you can check a few things:

- Make sure the processes are running. Use ps auxw to list all the running processes. Make sure you see the appropriate processes, regardless of whether the machine is a client, a server, or both.
- Check system logs (/var/log) to see if there are any messages indicating peripheral problems that could be affecting your configuration.
- If the processes appear to be running but not responsive, kill them and restart. In some circumstances, the daemon may be misbehaving and need to be restarted.
- Make sure /etc/nsswitch.conf is configured properly. This is a common problem.
- If you are trying to start the daemons by hand, make sure you are logged in as root.

When encountering problems, slow down, take a short break, and retrace your steps. It’s amazing how often simply slowing down helps you find problems.

# Summary

This chapter covered the installation and configuration of NIS master servers, secondary servers, and clients. In addition to the setup of NIS itself, common “NISisms” and netgroups are discussed. The lessons learned from these sections puts a powerful tool in your hands.

Some points to remember:

- Use ypint to set up NIS master servers and secondary servers.
- The /var/yp directory contains the Makefile necessary to update NIS information.
- Consider separating NIS files from your regular system files for clarity.
- NIS servers need the ypserv daemon.
- NIS clients need the ypclient daemon.
- yppasswdd allows users on NIS clients to change their passwords.
- Schedule a reboot to test all your changes.

![](img/cbac72550c7126a22162e94d91a0c360_498_0.png)

Although it isn't the most exciting feature to come along in recent history, NIS is one of the most useful of the core network services. In conjunction with other services, NIS gives you the ability to create a seamless system for all of your users.
