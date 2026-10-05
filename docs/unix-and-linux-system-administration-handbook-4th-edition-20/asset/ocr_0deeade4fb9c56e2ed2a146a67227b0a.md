use seem exactly in their approach. Some are simple but not secure and not scalable. Others are functional unwieldy. All the systems have limitations that prevent you from setting up the network the way you want to, and none of them manage all the information you may want to share across your machines.

In this chapter we first discuss some basic techniques for keeping configuration files synchronized on a network. Next, we address the Lightweight Directory Access Protocol (LDAP), a more sophisticated, platform-independent database system that is becoming a de facto standard in both the UNIX and Windows worlds. Most sites are migrating towards LDAP, in large part because Microsoft's adoption (of) the LDAP standard in their Active Directory product and the desire to better integrate Linux and Windows environments. Finally, we cover NIS, a popular database system that lingers in some environments but probably should not be deployed at new sites.

Note that sharing system files is different from system configuration and software deployment. These domains have different needs, and in practice, they are addressed by different solutions. See Chapter 12, *Installation and Management*, for details about going beyond that particular wall.

# 19.1 WHAT TO SHARE

Of the many configuration files on a UNIX or Linux system, only a subset can be usefully shared among machines. In modern times, the most pressing need for sharing relates to the contents of the **password**, **hosts**, and **aliases** files; however, other configuration files can become shared entities as well. Table 19.1 shows some of the most commonly shared files.

Table 19.1 System files that are commonly shared

| Filename | Function |
| --- | --- |
| /etc/passwd | User account information database |
| /etc/shadow* | Holds user account passwords |
| /etc/group | Defines UNIX groups |
| /etc/hosts | Maps between hostnames and IP addresses |
| /etc/mail/aliases | Holds electronic mail aliases |
| /etc/sudoers | Grants privileges for the **sudo** command |
| /etc/skel* | Holds default configuration files for new home directories |

+   a. Not necessarily sharable among flavors of UNIX since the encryption can vary; see page 179.

Table 19.1 is far from being a comprehensive list; your exact configuration depends on how similar you want the machines at your site to be. For the most part, though, additional configuration files are associated with specific applications and are not supported by administrative directory systems such as LDAP; you must share the files by copying them.