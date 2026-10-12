> **NOTE:** In most newsreaders, you see only the contents of some of the headers, such as the From and Subject headers. To see all the headers, you would have to open the news article in a text editor or choose some sort of view header function. See Chapter 9 for discussions of newsreaders.

Of the headers shown in the preceding example, several should be of interest to a news server administrator. The Path: header indicates where the article has already been sent. This lets your news server know that it doesn't need to forward an article to a host that appears there. The Newsgroups: header shows the newsgroup or newsgroups that the article is posted to. The Organization: is something that you need to set in your *inn.conf* file to identify your organization. Likewise, you need to set an *X-Complaints-To* value so that problems encountered by users of your server can be forwarded to you (or to whoever's e-mail the complaints related to your server are to be forwarded).

# # Configuring the INN server

The *inn.conf* file is where most of the general news server information is configured. For your INN news server to work, you must make several changes to this file. Most of the required changes are associated with identifying your server. However, you need to consider other changes that will have a major impact on how your server performs, what and how information is logged and stored, and the location of the directories that have newsgroup information. You add or change parameters in this file to configure INN.

After making a backup copy of the */etc/news/inn.conf* file, open it in any text editor and make changes based on the following descriptions.

> **TIP:** In general, you shouldn't remove parameters from the *inn.conf* file. If you aren't sure how to set a parameter, leave the default value, if one is given. More than 100 parameters are in the *inn.conf* file. For more on *inn.conf* parameters, see the *inn.conf* man page (type *man inn.conf*).

# ## General parameters

The *inn.conf* parameters described in this section identify your news server. They define the names of your organization and news server that appear in the header of local posts, the host path name that identifies how to get to your computer on the network, and the domain your computer is in. The following is a list of the *inn.conf* parameters along with a description of the values that you can set for each of these parameters:

+   - The *mta* parameter sets the particular mail transfer agent that is used by your news server to transfer messages. The following default setting causes the *sendmail* command to be used:
+     	mta:	/usr/sbin/sendmail -oi -oem $s
+   - The *organization* parameter identifies the name of your organization. When someone in your organization sends a news article, this name appears in the