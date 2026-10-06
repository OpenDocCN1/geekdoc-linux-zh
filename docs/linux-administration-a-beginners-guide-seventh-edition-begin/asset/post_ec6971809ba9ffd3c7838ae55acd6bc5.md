
## Changing Passwords with smpasswd

Users who prefer the command line over the web interface can use the smpasswd to change their Samba passwords. This program works just like the regular password program, except this program does not update the /etc/passwd file by default; instead, it updates Samba's user/password database.

smpasswd uses the standard Windows protocol/semantics for communicating with the server serving password changes. Therefore, using the right combination of parameters and options, you can cool the tool into changing a user password on a remote Windows server—from a Linux-based host!

To change your yang's Samba password, issue this command:

```bash
[root@server]# smpasswd yyang
```

Samba can be configured to allow regular users to run the smpasswd command themselves to manage their own passwords; the only caveat is that they must know their previous/old password.

> TIP You can use the pdbedit tool to change a user's Samba password. For example, to update the user yangyang's Samba password using pdbedit
> # pdbedit -a -u yyang

## Using Samba to Authenticate Against a Windows Server

Far far, we've been talking about using Samba in the Samba/Linux world. Or, to put it literally, we've been using Samba in its native environment, where it is lord and master of its domain (no pun intended). What this means is that Samba software stack, in combination with the Samba-server, has been responsible for managing all authentication and authorization issues.

The simple Samba setup that we created earlier in the chapter has its own database, which mapped the users to real Linux/UNIX users. This allowed any files and directories created by Samba to have the proper ownership contexts. But what if we want to deploy a Samba server in an environment with existing Windows servers are being used to manage all users in the domain? And we don't want to manage a separate user database in Samba? Enter the winbind daemon.

> NOTE Samba 4 is the latest and next-generation version of Samba. Among its enhancements, Samba 4 implements an Active Directory (AD)—compatible domain controller. It natively supports AD login and administrative protocols (Kerberos, LDAP, RPC, and so on). This means that all Windows clients can be transparently joined to a Samba 4 domain running on a Linux/UNIX-based Samba 4 server, and they will behave exactly as if they were members of native AD domain.

## winbindd Daemon

The winbindd daemon is used for resolving user accounts (users and groups) information from native Windows servers. It can also be used to resolve other kinds of system information. It is also able to do this through its use of pam_winbind (a PAM module that interacts with the winbindd daemon to authenticate users), libnss_winbind (winbind's Name Switch library) facility, and other relevant subsystems.

The process of setting up a Linux-based machine to consult a Windows server for its user authentication is also referred to as setting up Samba as a Member in an AD environment. The steps to achieve this are straightforward and can be summarized in this way:

1. Install the winbind software if it isn't already installed.
2. Configure Samba's configuration file (smb.conf) with the proper directives.
3. Add winbind to the Linux system's name switch facility (/etc/nsswitch.conf).
4. Join the Linux/Samba server to the Windows domain.
5. Test things.

Here present a sample scenario in which a Linux server serverA will use a Windows server for its user authentication needs. The Samba server is going to act as a Windows domain member.
The Windows server in this scenario is configured as a domain controller (as well as the DNS server). Its hostname is win-server and its IP address is 192.168.1.100. The short Windows domain name is WINDOWS-DOMAIN.

We have deliberately excluded any share definitions in this sample Samba configuration, and you'll have to create or specify your own (if you require it; see the earlier parts of the chapter for how to do this). Let's break down the process in detail:

1. Install the winbind package if it isn't already installed. In RPM-based systems such as Fedora, CentOS, or openSE, you can install it by issuing this command:

```bash
[root@fedora-server ~]# dnf -y samba-winbind
```

On Debian-based systems such as Ubuntu, you can install the package using this command:

```bash
master@ubuntu-server:~$ sudo apt-get install winbind
```

2. Create an /etc/samba/smb.conf file for Linux AD Member Server

```ini
# Sample smb.conf file for Linux AD Member
[global]
workgroup = WINDOWS-DOMAIN
password server = 192.168.1.100
security = ads
realm = WINDOWS-DOMAIN.COM
dedicated keytab file = /etc/krb5.keytab
kerberos method = secrets and keytab

```ini
idmap config * : backend = tdb
idmap config * : range = 1000-9999
idmap config WINDOWS-DOMAIN : backend = ad
idmap config WINDOWS-DOMAIN : schema_mode = rfc2307
idmap config WINDOWS-DOMAIN : range = 10000-9999
```

```ini
winbind nss info = rfc2307
winbind trusted domains only = no
winbind use default domain = yes
winbind enum users = yes
winbind expand groups = yes
winbind tickets = yes
winbind normalize names = yes
vfs objects = acl_xattr
acl inherit = yes
store attributes = yes
```

3. Edit the /etc/nsswitch.conf file on the Linux server so that it have entries similar to:

```text
passwd: winbind
shadow: winbind
group: winbind
```

4. Edit the /etc/resolv.conf file so that the Windows server is the primary DNS:

```text
search windows-domain.com
nameserver 192.168.1.100
```

5. Join the Samba server to the Windows domain using the net command. Assuming the Windows Administrator, use the following:

```bash
[root@fedora-server]# net join -S WINDOWS-DOMAIN -U Administrator
Joined FEDORA-SERVER to domain WINDOWS.COM
```

6. Next on Red Hat-like systems, you can use authconfig-tui utility to configure the other user information and authentication settings. Launch the tool from the command line and select Winbind over User Information. Select Winbind Authentication under Authentication, select Next, and finally select OK to save your settings.

7. On Linux distributions using systemd as the service manager, you can start the winbind daemon using the systemctl command:

```bash
[root@fedora-server ~]# systemctl start winbind
```

On versions (pre-systemd) of Debian-based distros, you can start the daemon by executing this command:

```bash
ubuntu-server:-$ sudo /etc/init.d/winbind start
```

8. Use the wbinfo utility (provided with the samba-winbind-clients package) to list all users in the Windows domain to make that things are working properly:

```bash
# wbinfo -u
```

That's it. The Linux server will now be able to consult and query the Windows Server for your user authentication needs.

## Troubleshooting Samba

The following are a few solutions to simple problems you might encounter with Samba:

- Restart Samba. This might be necessary because either Samba has entered an undefined state or (more likely) you've made major changes to the configuration but forgot to reload Samba so that the changes effect.
- Make sure the configuration options are correct. Errors in the smb.conf file are typically in directories, usernames, network numbers, and hostnames. A common mistake occurs when a new client is added to a group that has special access to the server, but Samba isn't told the name of the new client being added.
- Log files. Samba can be configured to generate as few as many logs as you want, and with varying levels of detail. The log files are your friend when troubleshooting Samba issues. Red Hat-like distros such as Fedora Samba-specific log files under the /var/log/samba/ directory. Keep a watchful eye on the logs!
