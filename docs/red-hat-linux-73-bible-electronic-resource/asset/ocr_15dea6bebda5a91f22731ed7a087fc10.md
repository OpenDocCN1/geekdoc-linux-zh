The line above identifies this configuration file as corresponding with the open-source Berkeley distribution of sendmail V9. The next lines refer to certain security features:

```
# override file safeties - setting this option compromises sys security
# addressing the actual file configuration problem is preferred
# need to set this before any file actions are encountered in cf file
#0 DontBlameSendmail=safe
```

This version of sendmail is, by default, somewhat paranoid, judging from the previous three commented lines. By not setting DontBlameSendmail=safe, sendmail won’t accept .forward files, include files, incoming mailboxes, configuration files, class files, or hashed map files that are group- or world-writable, or that are located in a directory that is group- or world-writable. If you need to override these defaults, you can remove the comment character (#) in front of the DontBlameSendmail line. The next lines relate to LDAP maps.

```
# default LDAP map specification
# need to set this now before any LDAP maps are defined
#0 LDAPDefaultSpec=-h localhost
```

With the LDAPDefaultSpec option, you can add default LDAP maps that include LDAP-specific settings. These settings apply to all LDAP maps, unless individual maps override those values. Set this option before you define any LDAP maps.

# ### sendmail local info entries

The next entries in the *sendmail.cf* file appear under the local info heading. They enable you to enter configuration information that is specific to your local host computer. Here are the first lines you see in that section:

```
##############
# local info  #
##############

Cwlocalhost
# file containing names of hosts for which we receive email
Fw/etc/mail/local-host-names
```

The previous lines have similar functions. The Cwlocalhost line defines the class macro w, which contains a list of all possible host names given to the machine. This includes any DNS aliases, all references in /etc/hosts, and perhaps even incorrect names used by individuals with accounts on that machine (to avoid having those messages bounced). Because this could become quite an extensive list on some hosts, the Fw/etc/mail/local-host-names line defines the file class macro w, which enables these host names to be stored in a separate file, /etc/mail/local-host-name in this case. The next lines are used to set your TCP/IP domain name:

```
# my official domain name
# define only if sendmail cannot automatically determine your domain
```