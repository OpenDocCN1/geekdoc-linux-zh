Note the warning that you shouldn’t edit the sendmail.cf file directly. In the rest of this section, the comments show which component m4 macro files (from subdirectories of the /usr/share/sendmail-cf directory) were used to create this sendmail.cf file.

The following setting from the sendmail.cf file indicates the version and vendor associated with the configuration file.

```
V10/Berkeley
```

The preceding line identifies this configuration file as corresponding with the open-source Berkeley distribution of sendmail V10. The next line refers to a certain security feature:

```
#O DontBlameSendmail=safe
```

This version of sendmail is, by default, somewhat paranoid, judging from the preceding commented lines. By leaving DontBlameSendmail=safe commented out, sendmail won’t accept forwarding files, include files, incoming mailboxes, configuration files, class files, or hashed map files that are group- or world-writable, or located in a directory that is group- or world-writable. (Set confDONT\_BLAME\_SENDMAIL to safe in the sendmail.mc file to override file safety checks.) The next line relates to LDAP maps.

```
#O LDAPDefaultSpec=-h localhost
```

With the LDAPDefaultSpec option, you can add default LDAP maps that include LDAP- specific settings. By default, none are set. Add a conf\_LDAP\_DEFAULT\_SPEC line to sendmail.mc to identify maps by host (-h host), port (-p port) or domain name (-d bindDN).

# sendmail local info entries

The next entries in the sendmail.cf file appear under the local info heading. They reflect configuration information that is specific to your local host computer. Here are the first settings in that section:

```
Cwlocalhost
Fw/etc/mail/local-host-names
```

The Cwlocalhost line defines the class macro w, which contains a list of all possible host names given to the machine. This includes any DNS aliases, all references in /etc/hosts, and perhaps even incorrect names used by individuals with accounts on that machine (to avoid having those messages bounced). Because this could become quite an extensive list on some hosts, the Fw/etc/mail/local-host-names line defines the file class macro w, which enables these host names to be stored in a separate file, /etc/mail/local-host-name in this case.

```
#Dj$w.Foo.COM
```

If you had set the confDOMAIN\_NAME in your sendmail.mc file, the preceding line would be uncommented and your domain name would replace Foo.COM. With this line commented,