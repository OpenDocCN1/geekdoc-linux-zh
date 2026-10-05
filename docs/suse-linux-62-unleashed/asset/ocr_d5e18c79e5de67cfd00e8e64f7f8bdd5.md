# Networking and Internet Services
PART II

2. If you allow other machines on your local area network or machines connecting through a remote access server on your machine to read news collected by your system, you need to add their names to the /etc/news/nnrp.access file. This file is read when the nnrp daemon starts for each person invoking a newsreader. The nnrp.access file contains a list of all the machines that are allowed to read news from your server and follows this syntax:

```
name:perms:password:newsgroup
```

name is the address of the machine that you are allowing to read news. You can use wildcards to allow entire subsets. perms is the permissions and one of the following values: Read (for read-only access), Post (to allow posting of messages), or Read Post (for both Read and Post). user authenticates a username before it is allowed to post, and password accomplishes the same task. To prevent a user from posting messages through your server, leave user and password as spaces so they can't be matched.

newsgroup is a pattern of newsgroup names that can be either read or not read, depending on how you set up the contents. Access to newsgroups uses wildcards, comp* allows access to all newsgroups starting with comp, where sex disables access to any newsgroups starting with the word sex. The default setting in the nnrp.access file is to prevent all access. To allow all users in the domain tpci.com to read and post news with no authentication required, add the following line to

```
*tpci.com:Read Post::*
```

To open the news system to everyone on your system regardless of domain name, use an asterisk of a domain name.

3. The inn.conf file should be in your /etc/news directory. You should probably change the line with organization in it to the following:

```
organization: Your company name
```

This specifies the default organization: header when your users to a newsgroup on your server.

Of course, if you are setting up IN to get news from your ISP's news server, ISP would have to set up its end with the newsgroups you want your users to be able to access. Remember that news takes a lot of bandwidth, so try to minimize the amount of news download.

After setting the incoming.conf, nnrp.access, and inn.conf files, and notifying your ISP that you want to use NNTP service, you should be able to use IN to download news and access it with a newsreader. (This assumes you've granted yourself permission in the nnrp.access file.) A lot of complexity can be introduced into INN's configuration file, but