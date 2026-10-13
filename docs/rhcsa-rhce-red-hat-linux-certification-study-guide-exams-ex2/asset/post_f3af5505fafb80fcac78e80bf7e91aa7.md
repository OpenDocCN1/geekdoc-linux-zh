
While OpenLDAP does support the SHA512 passwords now included by default in the shadow password suite, the default is based on MD5 hashes.

```
pam_password md5
```

If you prefer the SHA512 hash, replace that directive with:

```
pam_password exop
```

## /etc/openldap/ldap.conf

You'll need to specify the URI, BASE, and TLS_CACERTDIR variables in this file, just as was done in the /etc/pam_ldap.conf configuration file. Given the parameters in the preceding section, you may even see a fourth directive in that file:

```
URI ldap://127.0.0.1
HOST testrl.example.com
BASE dc=example,dc=com
TLS_CACERTDIR /etc/openldap/cacerts
```

If the LDAP server is not on the local system, and the network domain is not example.com, substitute accordingly. Individual users can supersede this file in a hidden .ldaprc file in their home directories.

## The Name Service Switch File

The Name Service Switch file, /etc/nsswitch.conf, governs how a computer searches for key files such as password databases. It can be configured to look through LDAP and other server databases. For example, when an LDAP client looks for a computer host name, it might start with the following entry from /etc/nsswitch.conf:

```
hosts: files ldap dns
```

This line tells your computer to search through name databases in the following order:

- 1. Start with the database of host names and IP addresses in /etc/hosts.
- 2. Search for the host name in a map file based on LDAP.
- 3. If none of these databases includes the desired host name, refer to the DNS server.

You can configure the /etc/nsswitch.conf configuration file to look at an LDAP server for the desired databases. For example, to set up a centralized username and password database for your network, you'll need to configure at least the following commands in /etc/nsswitch.conf:

```
passwd:  files ldap
shadow:  files ldap
group:   files ldap
```

Other authentication databases can be configured; NIS is associated with the nis directive; Microsoft authentication before LDAP-based AD services is associated with winbind.

## Red Hat Network Authentication Tools

If you're not familiar with LDAP, it may be simpler to configure a system with the Red Hat Authentication Configuration tool. In RHEL 6, you can start it in the GUI with the system-config-authentication command or in the console with the authconfig-tui command. This opens an Authentication Configuration tool; the GUI version is shown in Figure 8-4.

The Authentication Configuration tool has changed. By default, it's set to look at only the local authentication database. But if you click the drop-down text box, it presents three other options. LDAP is all that matters under the current

![](img/9139201cfcaf4292284a0eed074928e5_491_0.png)

RHCSA objectives. When selected, the window changes, as shown in Figure 8-5. It defaults to the Kerberos Password Authentication Method, associated with client authentication under that system discussed in Chapter 11.

So if you see Kerberos in the window, click the associated text box, and select LDAP Password. The window changes again, and provides the following warning:

```
You must provide ldaps:// server address or use TLS for LDAP authentication.
```

To eliminate that warning, select the Use TLS To Encrypt Connections option. If successful, what you see should resemble Figure 8-6.

This section assumes you're using LDAP as the User Account Database. The Authentication Configuration tool requires you to select the Use TLS To Encrypt Connections option. Those options won't be changed.

## FIGURE 8-5

- LDAP
- Authentication
- Configuration
- Options

![](img/9139201cfcaf4292284a0eed074928e5_492_0.png)

## FIGURE 8-6

LDAP
Authentication
Configuration
Options

![](img/9139201cfcaf4292284a0eed074928e5_493_0.png)

The remaining options may vary:

- 1. The LDAP Search Base DN text box includes the domain name for the LDAP server. For example, if the local system domain is my-domain.com, the text box should contain the following:
- 2. The LDAP server text box should include the URI of that server. If it's the local computer, you can use the 127.0.0.1 IP address. But that's unlikely, especially on an exam.
- 3. If LDAP is associated with a Certificate Authority (CA) certificate, click Download CA Certificate. It opens a window that allows you to specify the URL with the CA Certificate with the .pem extension.

```
dc=my-domain,dc=com
```

Now select the other tab, Advanced Options. The options are shown in Figure 8-7. It's just for reference, and not related to the configuration of an LDAP client.

## FIGURE 8-7

- Advanced
- Authentication
- Options

![](img/9139201cfcaf4292284a0eed074928e5_494_0.png)

Once you've made desired changes, click OK; it may take a few seconds for the Authentication Configuration tool to write the changes to the noted configuration files.

## CERTIFICATION OBJECTIVE 8.05

### Special Groups

In the past, Linux groups of regular users allowed its members to share files. Red Hat has helped change this with the way it assigns unique UID and GID numbers to each user. When regular users are all made members of the same group, that also means everyone in that group has access to the home directories of all other group members. And that's often not desirable. Users may not want to share the files in their home directories with others.

On the other hand, RHEL gives each user a unique user ID and group ID in /etc/passwd. This is known as the user private group scheme. Users get exclusive access to their own groups and don’t have to worry about other users reading the files in their home directories.

### Standard and Red Hat Groups

In RHEL, each user gets her own special private group by default. As noted earlier, UIDs and GIDs normally start at 500, are assigned matching numbers, and proceed in ascending order. In addition, you can set up special groups of dedicated users, ideally with higher GIDs. For example, an administrator might configure accgrp for the accounting department, perhaps with a GID of 70000.

### Shared Directories

Most people work in groups. They may want to share files. There may be good reasons for people in those groups to keep their information hidden from others. To support such groups, you can set up a shared directory, with access limited to the members of that group.

Assume you want to set up a shared directory, /home/accshared, for a group of accountants. To that end, you can set up a shared directory with the following basic steps:

- 1. Create the shared directory:
  ```
  # mkdir /home/accshared
  ```
- 2. Create a group for the accountants. Call it accgrp. Give it a group ID that doesn’t interfere with existing group or user IDs. One way to do this is to add a line such as the following to the /etc/group file, or with the User Manager. Substitute desired usernames.
  ```
  accgrp:x:70000:robertc,alann,victorb,roberta,alano,charliew
  ```
- 3. Set up appropriate ownership for the new shared directory. The following commands prevent any specific user from taking control of the directory and assign group ownership to accgrp:
  ```
  # chown nobody.accgrp /home/accshared
  # chmod 2770 /home/accshared
  ```

Any user who is a member of the accgrp group can now create files in and copy files to the /home/accshared directory. Any files generated within or copied to that directory will be owned by accgrp group.

This is made possible by the 2770 permissions that assigned to the /home/accshared directory. Break that down into its component parts. The first digit (2) is the set group ID bit, also known as the SGID bit. When a SGID bit is set on a directory, any files created in that directory automatically have their group ownership set to be the same as the group owner of the directory. In addition, group ownership of files copied from other directories is reassigned, in this case, to the group named accgrp. There is a second way to set the SGID bit for the /home/accshared directory:

```
chmod g+s /home/accshared
```

The remaining digits are basic knowledge for any experienced Linux or Unix user. The 770 sets read, write, and execute permissions for the user and group that own the directory. Other users get no permissions to that directory. But since the user owner of the directory is the nonprivileged user named nobody, the group owner of the directory is most important. In this case, members of the accgrp group have read, write, and execute permissions to files created in this directory.

## EXERCISE 8-5

### Control Group Ownership with the SGID Bit

In this exercise, you will create new files in a directory designed to be shared by a group of users. You'll also see the difference in what happens before and after the SGID bit is set.

- 1. Add users called test1, test2, and test3. Specify passwords when prompted. Check the /etc/passwd and /etc/group files to verify that each user's private group was created:
  ```
  # useradd test1; passwd test1
  # useradd test2; passwd test2
  # useradd test3; passwd test3
  ```
- 2. Edit the /etc/group file and add a group called tg1. Make the test1 and test2 accounts members of this group. You could add the following line to /etc/group directly or use the Red Hat User Manager:
  ```
  tg1:x:99999:test1,test2
  ```
