# FIGURE 17.3

Enter the name of the news server here.

![](bbox=[0.22, 0.12, 0.46, 0.3])

+   6. If you have more than one news server set up, highlight the one you want to use as your default and click the Set as Default button.
+   7. Click OK to exit the preferences dialog and save your settings.
+   8. Now you are ready to read news using Netscape Communicator.

Just use the Newsgroup reader component of Netscape Communicator to subscribe to the newsgroups that you are interested in.

**CAUTION**
The first time you subscribe to a newsgroup, you must open it. It will be completely empty except for one message from leafnode itself—this is ok. Now that you've opened it, leafnode has registered that it will collect the articles in this newsgroup the next time fetchnews is run. That's why you should open the newsgroups you subscribed to in order to tell leafnode to fetch their articles. This is only needed the first time you subscribe to a newsgroup.

You now can use any news client on any platform to access your news server. Multiple connections to the server are also allowed, of course.

# Troubleshooting

*When I attempt to connect to my news server, using either telnet or a news client, the connection fails.*

Make sure that you did install leafnode from the SuSE CDs and that you enabled it in /etc/inetd.conf.

*I connected to the news server using my news client, but I see no newsgroups at all.*

You have to run fetchnews before any clients connect to leafnode for the first time. This command fetches the newsgroups listing from the remote news server. Any clients who connected to leafnode before this command was run won't see any newsgroups.