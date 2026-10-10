The Linux system you're configuring must be accessible under two different hostnames (`www.pangaea.edu` and `www.mesozoic.edu` in this example). This configuration normally requires editing DNS server entries; however, you might be able to achieve the same effect by editing the `/etc/hosts` file on your client computer.

# Caveats

The usual **root**-access cautions apply to this task. In addition, Web servers are unusually visible network servers. Crackers frequently attack Web server computers, and if the Web server software (or any other server running on the computer) is buggy or misconfigured, the result can be a serious compromise of the computer. This can lead to defacement of your Web pages, theft of your data, use of your system for further attacks on your own or other networks, and so on. For this reason, you should be very cautious about configuring a Web server. If you don't need to run Web server software on your computer, you should shut it down or, better yet, uninstall the software when you're done with this task. As a general rule, if you're running a Web server on the Internet at large, you should learn more about Apache than you can learn from this task alone. If you want to run Apache on a well-protected computer on a local network (say, behind a NAT router for use by local users), the risks are much less substantial.

# Procedure

To complete this task, you must first prepare directories for storing your Web pages. You should then find and understand the Apache configuration files. You can then configure Apache to use the directories you've created, both for the main domain Web pages and for user Web pages.

# Preparing Your Web Space

The scenario for this task specifies that the `/var/web/pangaea` and `/var/web/mesozoic` directories should hold the Web pages for the two main Web sites hosted by your Web server. You can create these directories using ordinary Linux directory-creation commands:

```
```
# mkdir -p /var/web/pangaea
# mkdir /var/web/mesozoic
```
```

The `-p` option on the first command ensures that the `/var/web` directory will be created if it doesn't already exist. When you create these directories as **root**, they'll be owned by **root** and, in all probability, other users won't be able to create files in them. Chances are other users have been tasked with creating the actual Hypertext Markup Language (HTML) files that make up each Web site. Thus, you might want to change the ownership, group ownership, or permissions of these directories to enable other users to write to them. For instance, suppose the computer has a **wmaster** group and users of this group should be able to modify Web pages. You might enable this access by changing ownership and permissions in this way:

```
```
# cd /var/web
# chgrp wmaster mesozoic pangaea
# chmod 0775 mesozoic pangaea
```
```