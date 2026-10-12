# Adding the newsgroups

The final step is to add the newsgroups. After you have configuration files updated and `inn` running, it's very easy to add a local newsgroup. Log in as `root` and use `ctlinnd` to perform this task. For example, here's how you add a newsgroup named `xyz.general`:

```
/usr/lib/news/bin/ctlinnd newgroup xyz.general
```

That's it! That command adds the `xyz.general` newsgroup to your site. If you use the traditional storage method, the `inn` server creates the directory `/var/spool/news/articles/xyz/general` and stores articles for that newsgroup in that directory (this happens the first time someone posts a news article to that newsgroup).

After you've created all the local newsgroups, users from your intranet should be able to post news articles and read articles in the local newsgroups. If they have problems accessing the newsgroups, make sure that the `/etc/news/readers.conf` file contains the IP addresses or names of the hosts that should be able to access the `inn` server.

# Testing your newsgroups

For example, I add a newsgroup named `local.news` on an INN server running on my Red Hat Linux system by using the instructions explained in the previous sections. Then I start Mozilla on another Red Hat Linux system on the LAN and set up a new news account with the news server set to my INN server. Next, I access the `local.news` newsgroup by typing `news:local.news` as the URL. Try it! I bet you'll like it.