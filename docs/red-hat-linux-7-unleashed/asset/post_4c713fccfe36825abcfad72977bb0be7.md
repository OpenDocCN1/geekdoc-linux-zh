
## Understand the Access Hierarchy

Samba requires a functioning network, meaning you can't Samba if you can't ping. A “Samba problem” is not really a Samba problem if you can't ping—it's a network problem. Likewise, you can't browse on a Windows client if you can't browse (via smbclient -NL servername) on the Linux server. So if Windows browsing doesn't work, check browsing on the server.

Additionally, you can't browse in Network Neighborhood if you can't browse in the Windows command environment via the net view \servername command. The bottom line is to be conscious of the following access hierarchy:

- You must be able to ping to be able to browse on the server.
- You must be able to browse on the server to browse on the Windows client's command line.
- You must be able to browse on the Windows client's command line to be able to browse in Network Neighborhood or Windows Explorer.

## Look at the Log Files

Samba writes its activity to its log files. The default location for its log files on a Samba server are contained in directory /var/log/samba. By viewing these logs you can look back in time to see what transpired during the error.

Additionally, most Samba software can be run at higher error levels such that more debugging information is written to the logs. This can greatly aid diagnosis. See the various man pages for methods of increasing error levels.

## Use SWAT to Reduce Your smb.conf File

Comments are nice documentation, and so are parameters explicitly set to their default values. But too much of such “readability” makes for an incredibly unwieldy and therefore unreadable smb.conf. Sometimes it's nice to get rid of all the comments and the parameters set explicitly to their default values. SWAT does just that. Simply back up your existing smb.conf (this is a must), and then run SWAT as root, enter the global page, and click the Commit Changes button. All comments and explicitly specified defaults disappear, leaving just the system's distinctive features.

## Making a Sure-Fire Browser from smb.conf

Sometimes you just can't see the Samba server from your Windows 9x machines. This is especially prevalent when there is no WINS server, domain master, or PDC on the network. If there are no NT or Windows 2000 servers (or clients acting as WINS servers or PDCs), you can guarantee the Samba box becomes a WINS server and browse master by including the following:

```
os level=65
preferred master=yes
domain master=yes
```

**Caution**

Never use the preceding settings on a network that has an NT or Win2K master browser, WINS server, or PDC. To do so will cause serious network problems.

Also, make sure to set the netbios name= parameter to the hostname of the Samba server, and to set the workgroup= parameter to the workgroup of the client computers.

## Keep a Cool Head

Troubleshooting is easy with the right attitude. Simply hunt down the root cause with a “just the facts” attitude. You can see a detailed description of troubleshooting and troubleshooting processes at http://www.troubleshooters.com/tuni.htm.

## Samba Security

Lock up your smb.conf file, and throw away the key. Giving a person write access to smb.conf is as good as giving him the root password. Here’s why.

Imagine a disgruntled employee writing a script that backs up /etc/passwd and then creates an /etc/passwd file with no root password. He logs in as root, without a password, and now has control of your system. He restores the original /etc/passwd and changes the password again.

But of course the script mentioned in the preceding paragraph won’t work unless he’s running as root. So he writes the script, manages to get write access to smb.conf, and adds a new share with a root preexec= option pointing to his mischievous script. He then accesses his new share through Samba, and immediately logs in as root and changes the password. He covers his tracks, and owns the system. Unbelievably, he didn’t need to restart Samba to accomplish this exploit.

The root preexec= and root postexec= parameters run the commands specified by their values as root. This functionality cannot be turned off without a source code change to Samba. Therefore, the utmost care must be taken to grant smb.conf write access only to those who can be trusted with the root password. Making smb.conf owner root, group root, file mode 644 should do the trick.

**Caution**

It might seem a good idea to make the file mode 664, and then give a select group access to smb.conf. Unfortunately, older versions of SWAT enabled complete read/write access to an smb.conf that was owned by root, group root, and file mode 660 or 664. The SWAT that comes with Red Hat 7 does not have this flaw, but a cracker might be able to install the older SWAT on the system, after which he could exploit this flaw.

## SWAT Precautions

SWAT is the smb.conf configuration program with a browser interface, discussed later in the section titled “Using SWAT for Web-Based Samba Configuration.” The preceding caution statement highlights one of the security issues with SWAT. There are others. All passwords given to SWAT are sent in the clear, so they can be sniffed. That’s why it’s best to allow SWAT only from localhost.

Another SWAT precaution is to shut down all sessions of your browser after completing your SWAT work. A SWAT authentication remains good as long as there’s a session of the browser. That means you could finish your SWAT work, navigate out of the SWAT Web pages, and even close the browser. But if there are other copies of the browser running, a sneaky co-worker could sit down at your computer, navigate to `http://192.168.100.1:901` (or wherever your Samba server resides), and install a mischievous `root_preexec=` parameter while you’re gone.

## Considerations for Special Parameters

Several parameters deserve a security mention. Certainly the `hosts equiv=` parameter should never be used, because it specifies a file listing hosts and users who are allowed on without passwords.

In anything but the most trusting environments, or servers with nothing but printers, `security=share` should not be used because passwords relate to shares, not users. That means when an employee leaves, he leaves with the passwords to the shares. It also means that passwords are known far and wide.

Watch out for the `admin users=` parameter. It grants users listed in its value total access to the share’s entire tree. Although they are confined to that tree, they can still do plenty of damage if mistakes are made. Don’t use `admin users=` unless you have a very good reason to do so, and can’t do what is needed any other way.

The `valid users=` parameter is a good thing. It restricts share access to those on its list. Because groups can be put in that list, you should use a `valid users=` parameter in all shares except those you truly want to be universally accessible, or in special shares like [homes], [printers], and [netlogon].

Use `writable=`, `read list=`, and `write list=` to determine which users and groups have write access.

The hosts `allow=` parameter can limit access to certain subnets or hosts. Use it.

## This Is the Tip of the Iceberg

Security is an immense subject. This section has presented a few of the most obvious security issues. There are hundreds of other issues, including password synchronization, LDAP, NIS, SSL, Kerberos, checking the authenticity of your Samba source code or RPM package, and much, much more. Samba Unleashed contains an entire chapter on Samba security, and for the system administrator needing to lock things down really tight, there's plenty to learn beyond that.

## Using SWAT for Web-Based Samba Configuration

SWAT is a Web-based tool to provide local or remote, password-guarded Samba administration from any browser that can access the server. SWAT is new with Samba 2 and is included in Red Hat 7, which ships with Samba 2.0.7.

## Caution

Configuring with SWAT will dramatically change your smb.conf file. It will eliminate all comments, eliminate `include=` and `copy=` options, eliminate many options already set to the default, and change options to more common synonyms (and in some cases to inverse synonyms, simultaneously reversing the value).

Always back up smb.conf before configuring with SWAT. A SWAT-configured smb.conf file is much shorter, making it more readable. However, the loss of comments and self-documenting default-configured options can make it less readable. If you've tailored your smb.conf for readability and self-documentation, you may want to refrain from using SWAT.
