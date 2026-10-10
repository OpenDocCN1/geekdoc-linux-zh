name is the address of the machine that you are allowing to read news. (You can use wildcards to allow entire subnets.) perms is the permissions and has one of the following values: Read (for read-only access), Post (to allow posting of messages), or ReadPost (for both Read and Post). The user field is used to authenticate a username before it is allowed to post, and password accomplishes the same task. To prevent a user from posting messages through your server, leave user and password as spaces so that they can’t be matched.

The newsgroup field is a pattern of newsgroup names that can be either read or not read, depending on how you set up the contents. Access to newsgroups uses wildcards, so comp.* allows access to all newsgroups starting with comp, whereas !sex disables access to any newsgroups starting with the word sex. The default setting in the innrp.access file is to prevent all access. To allow all users in the domain tpci.com to read and post news with no authentication required, you add this line to innrp.access:

```
*.tpci.com:Read Post:::*
```

To open the news system to everyone on your system regardless of domain name, use an asterisk instead of a domain name.

+   3. The file inn.conf.sample should be in your /etc/news directory. Copy this file to inn.conf and change the line with organization in it to:

```
organization:    Your company name
           pathhost:    your FQDN
```

This specifies the default for the organization header for those newsgroup users who use your server.

Of course, if you are setting up INN to get news from your ISP’s news server, your ISP would have to set up their end with the newsgroups that you want your users to be able to access. Remember that news takes up a lot of bandwidth, so try to minimize the amount of news you download.

As noted, the innd daemon monitors port 119 for NNTP activity regarding floods and batchers, but it also has another function related to a different protocol. The innd daemon also listens for NNRP (Net News Read Protocol) activity coming in from Usenet reader software.

As your server continues efficiently serving Usenet newsgroups, accepting or rejecting posts, filtering unwanted messages or groups, and performing other housekeeping tasks, you must carefully watch the output of the monitoring tools to see how your available disk space is accommodating the load.

If your INN server is showing signs of unacceptably high load (known to be slowing down all machine functions or compromising disk space), an INN administrator will