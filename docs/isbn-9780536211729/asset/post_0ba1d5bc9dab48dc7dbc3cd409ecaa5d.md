
## 3.4.1.7 Executables and Dynamic Libraries

```bash
cd /home/ftpusers
mdir joe sally
chgrp users joe sally
chown joe joe
chown sally sally
ln -s /home/ftpusers/joe /home/joe/ftp
ln -s /home/ftpusers/sally /home/sally/ftp
```

- `-d` causes debugging information to be logged by the syslog facility.
- `-a` causes the ftpaccess() file in /etc to be used to control FTPD's configuration. This allows much more detailed configuration. A typical entry for ftp in /etc/inetd.conf would be:

```text
ftp stream tcp nowait /usr/sbin/tcpd.ftp -l -i -a
```

When an ftp user uses the command `ls` or its synonym `nls`, ftpd invokes the `ls` Linux command to generate the data that ftpd sends back to the user. The problem is that the ftpd daemon is running in a chrooted environment (where it normally does for anonymous FTP access), it does not have access to `/bin/ls` nor to any dynamic libraries that `ls` would use. The solution is to put `ls` in `~ftp/bin` and provide any dynamically linked libraries that it might need in `~ftp/lib`. Most distributions such as Red Hat do this and Red Hat even offers an anonymous FTP RPM containing these programs and dynamic libraries.

All needed files should be installed on your system already if you asked for the appropriate packages to be loaded. Slackware builds a special statically linked program that is installed as `~ftp/bin/ls` so that the SysAdmin does not need to bother with dynamic libraries. Red Hat does not do this but it puts `tar` and `gzip` in there so that ftpd automatically can convert between compressed and uncompressed files and tar and untar data too. It includes the shell, `sh`.

I worry that the presence of this apparently unrestricted shell opens a security hole. I might prefer the Slackware solution. Of course, because it is Linux, you can put the Slackware `~ftp/bin` program on your otherwise Red Hat system, after removing the Red Hat programs and dynamic libraries from `~ftp/bin` and `~ftp/lib`, and it should work just fine. This is assuming that the version of the Slackware `ls` program is compatible with the version of the Red Hat kernel. This is usually not a problem and if it is then it will refuse to run.

I have compiling a complex CGI C program on Slackware and running it on many different versions of Red Hat and Mandrake for six years to work around a bug in Red Hat's `ctime()` library, now fixed.

## 3.4.1.8 Allowing Controlled Uploading

Allowing public anonymous uploading generally is a bad idea. When allowed, crackers and other undesirables discover this quickly and use your site for their evil purposes. This will usually be to crack systems, pornography (no doubt different from any that you might be interested in), and other things that you do not want on your system. If you choose not to allow uploading, simply have the directories 755 (or 555) and owned by ftpdadmin. Then, the ftp user, known as anonymous, will be prevented from uploading any pages.

If you choose to have an unrestricted upload facility, the convention is to have `~ftp/incoming` directory for this purpose and for it to be owned by ftpdadmin. For full access it should be mode 777 but this is not recommended if the system is accessible from the Internet; possibly, the directory is checked frequently for undesired files and removed promptly. An alternative would be to have the file mode 733. This means that the owner, ftpdadmin, has full access but others have only write and execute access. This account, ftpdadmin, should be different from the account that is used for anonymous FTP login, typically ftp. This allows the anonymous user to upload files ftp users cannot see what is in that directory, preventing the directory from being used for public exchange.

Certainly, the person uploading can tell others the file name and then they could download it. A solution would be to periodically "sweep" these files into a different directory that is not accessible at all by ftp, via a cron job. The sweep directory might be `~ftp/sweep`, owned by ftpdadmin and mode 700. This is a simple ftpdadmin cron job to sweep files into this directory hourly. It does not have protection against a file overwriting an earlier file of the same name but then this will allow someone to update a submission.

```bash
* * * * * /bin/mv /home/ftp/incoming/* /home/ftp/sweep/ > /dev/null 2>&1
```

Some sites will have `~ftp/incoming` mode 711 with subdirectories of secret names being named 733. Someone wanting to upload a file will first have to ask the SysAdmin for the name of one of these secret directories and upload to it, but I do not see that this is a significant improvement on the method discussed earlier and requires more overhead.

## 3.4.2 FTP Proxy Dangers

![image](img/7d04225c75a86d3cf4bd6077596f35b2_166_0.png)

Older FTP servers allow a client to request that the server do operations to any arbitrary third system. This allowed a variety of security breaches, including sending e-mail that appears to come from an FTP server's system and tunneling through firewalls. If your FTP server was inside your network and the firewall allowed Internet access only to your FTP server, the proxy feature then could be used to access any system inside the firewall. The nmap network mapper can make use of this feature to probe behind firewalls. To see if Pentacorp’s FTP server is vulnerable, assuming that Pentacorp has the class A network 10.0.0.0/8, the following command could be used:

```bash
nmap -F -e eth0 -b ftp.pentacorp.com 10.0.0.0/8
```

If your FTP server does not allow this, you will see this message:

> Your FTP bounce server [censored], it won't let us feed bogus ports!

Since Red Hat 6.0, the FTP server generates this message and is safe. Other firewall tunneling dangers are discussed in “Tunneling Through Firewalls” on page 71.

## 3.5 The rsh, rcp, rlogin, and rexec Services

![image](img/7d04225c75a86d3cf4bd6077596f35b2_167_0.png)

In “Turn Off rsh, rcp, rlogin, and rexec” on page 94 it was recommended that these services are turned off because they are not considered secure and that SSH is an excellent alternative. Because these services are so popular (because they are useful), an explanation about how they work and their insecurity is offered here.

> The rsh, rcp, rexec, and rlogin services are too insecure and too dangerous to use. Remove them from your systems and forbid their use. Really.

These allow one to remotely execute a process. In other words an account named joe on remote system zoro.com can issue the command:

```bash
rsh pentacorp.com stab files
```

This will ask that pentacorp.com execute the command `stab files` as account joe. The authentication (to verify that this request is allowed) is by looking up the initializing system's name and account name (zoro.com and joe) in two configuration files on the pentacorp.com system.

If the initializing system’s name appears in the system-wide configuration file `/etc/hosts.equiv`, any request from a user name on that system to pentacorp.com for the same user name will be honored. In other words, if the entry:

```text
zoro.com
```

appears in `/etc/hosts.equiv` on pentacorp.com, any user on zoro.com can do rsh commands with the same user name as pentacorp.com. Thus, zoro.com user joe can have commands executed by user joe on pentacorp.com and cindy on zoro.com can have commands executed by user cindy on pentacorp.com but given permission by `/etc/hosts.equiv` to execute commands as cindy on pentacorp.com and vice versa. Individual users may grant additional permissions for remote users to operate under their accounts. This is done by creating the file `.rhosts` in their home directory and adding the desired entries. Each entry takes up a line and may be in either of two formats.

The first format lists just the host name of the remote system allowed to rsh. Thus, if cindy's home Linux box is hv.isp.com and her personal account on it also is cindy she could add the entry:

```text
hv.isp.com
```

to her `.rhosts` file. Suppose cindy also is taking a night class at Georgia Tech and her account is cc02 on cory.gatech.com. She cannot specify cory.gatech.com because the account is different. Instead she specifies the host name, a space, and the remote account as such:

```text
cory.gatech.com cc02
```

If she is also taking a class on comparative religion and that account is cr72, her `.rhosts` file might look like:

```text
hv.isp.com
cory.gatech.com cc02
cory.gatech.com cr72
```

The daemons for rsh and rexec have several security features to reduce intrusions.

- 1. In order for `in.rshd`, the server that supports rsh and rcp, to consider a user's `.rhosts` file, it ensures that the file is owned by the user and nobody else has write access to it. Thus, permissions of 600 or 644 are acceptable but not 666.
- 2. The `in.rshd` daemon also performs a reverse lookup on the numeric IP of the system making the request. This means that it takes the numeric IP address and determines what host name has that address. It requires that this host name matches the one that the requesting system claims to be. This prevents a cracker from issuing the command:

```bash
hostname zoro.com
```

With a system in your own domain, you must list it in the `.rhosts` or `hosts.equiv` in the same way the reverse lookup shows it (either fully qualified
