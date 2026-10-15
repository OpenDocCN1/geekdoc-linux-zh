
winbind -g to see groups. The command getent passwd shows the user accounts defined in all sources, in /etc/passwd format:

```
ubuntu$ getent passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
...
bwhaley:x:1006:10018::/home/bwhaley:/bin/sh
guest:x:10001:10001:Guest:/home/ULSAH/guest:/bin/bash
ben:x:10002:10000:Ben Whaley:/home/ULSAH/ben:/bin/bash
krbtgt:x:10003:10000:krbtgt:/home/ULSAH/krbtgt:/bin/bash
```

The only way to distinguish local users from domain accounts is by user ID and by the ULSAH path in the home directory, apparent in the last three entries above. If your site has multiple domains or if the winbind use default domain option is not set, the short domain name is prepended to domain accounts (for instance, ULSA\ben).

## PAM configuration

At this point the system has been configured to communicate with Active Directory through Samba, but authentication has not been configured. Setting up PAM to do authentication through Active Directory is a bit tricky, mostly because the specifics differ widely among Linux distributions.

The general idea is to configure winbind as an authentication module for all the services that should have Active Directory support. Some distributions, such as Red Hat, conveniently set up all services in a single file. Others, such as Ubuntu, rely on several files. Table 30.1 lists the appropriate files for each of our example Linux distributions.

See page 908 for general information about PAM.

### Table 30.1 PAM configuration files for winbind support

| System | Authentication | Session |
|---|---|---|
| Ubuntu | common-account, common-auth, sudo | common-session |
| SUSE | common-auth, common-password, common-account | common-session |
| Red Hat | system-auth | system-auth |

To enable winbind authentication, add

```
auth sufficient pam_winbind.so
```

at the beginning of each file. An exception is SUSE's common-password file, in which you must replace the auth keyword with password:

```
password sufficient pam_winbind.so
```

PAM can create home directories automatically if they don't exist when a new (to the system) user logs in. Since Active Directory users aren't added by the standard useradd command, which is normally responsible for creating home directories, this feature is quite helpful. Add the following line to PAM’s session configuration file as indicated in Table 30.1:

```
session required pam_mkhomedir.so umask=0022 skel=/etc/skel
```

With this configuration, PAM creates home directories with octal permissions 755 and with autoupdates copied from /etc/skel.

You may also want to restrict access to the local system to users who are in a particular Active Directory group. To do that, add the following line to PAM’s session configuration file:

```
session required /lib/security/$ISA/pam_winbind.so use_first_pass
    require_membership_of=unix_users
```

Here, only users in the AD group unix_users can log in.

## Alternatives to winbind

Although the “free as in beer” route to Active Directory clienthood outlined above works well enough, it is error prone and riddled with complexity. Alternatives exist for administrators who want a relatively painless installation and troubleshooting support from a knowledgeable third party.

Products from Likewise Software automate **winbind**, name service switch, PAM, and identity mapping configuration for more than 100 Linux distributions and UNIX variants, including all the example systems referenced in this book. Likewise also includes a group policy object agent, which permits some centralized configuration for AD-enabled UNIX systems. Several GUI plug-ins, including a management console and an Active Directory snap-in, simplify installation and configuration. A limited version is available for free, or you can pay for support and complete functionality. Find details at likewise.com.

Another option that skirts **winbind** entirely is a tool kit called Quest Authentication Services. It offers many of the same features as Likewise’s tools, but adds additional group policy management features. Be prepared to open your wallet, as Quest’s tools do not come cheap. See quest.com/authentication-services for the full scoop.

## 30.10 RECOMMENDED READING

TERPSTRA, JOHN H. *Samba-3 by Example: Practical Exercises to Successful Deployment (2nd Edition).* Upper Saddle River, NJ: Prentice Hall PTR, 2006. (An on-line version of this book is available at samba.org.)

TERPSTRA, JOHN H., JELMER R. VERNON. *The Official Samba-3 HOWTO and Reference Guide (2nd Edition).* Upper Saddle River, NJ: Prentice Hall PTR, 2006. (An on-line version of this book is available at samba.org.)
