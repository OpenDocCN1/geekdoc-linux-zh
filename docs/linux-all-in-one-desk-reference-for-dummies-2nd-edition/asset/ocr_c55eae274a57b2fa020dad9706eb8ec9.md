+   3. **Add a storage method to use for the local newsgroups.**  
+   For example, you can add the following lines in `/etc/news/storage.conf` to define the storage method for the new *xyz* hierarchy of newsgroups (change *xyz* to whatever you name your local newsgroups):
+   ```
+       method tradspool { 
+           class: 1
+           newsgroups: xyz.* 
+       }
+   ```
+   4. To make these changes effective, restart the news server (Type **service inn restart** in Fedora Core or **/etc/init.d/inn restart** in Debian, MEPIS, SUSE, Ubuntu, and Xandros.)

# Adding the newsgroups

The final step is to add the newsgroups. After you update the configuration files and run *innd*, adding a local newsgroup is easy. Log in as *root* and use `ctlinnd` to perform this task. For example, here's how you add a newsgroup named *xyz.general*:

```
``` /usr/lib/news/bin/ctlinnd newgroup xyz.general ```
```

That's it! That command adds the *xyz.general* newsgroup to your site. If you use the traditional *storage* method, the *innd* server creates the directory `/var/spool/news/articles/xyz/general` and stores articles for that newsgroup in that directory. (This happens the first time someone posts a news article to that newsgroup.)

After you create all the local newsgroups, users from your intranet can post news articles and read articles in the local newsgroups. If they have problems accessing the newsgroups, make sure that the `/etc/news/readers.conf` file contains the IP addresses or names of the hosts that have access to the *innd* server.

# Testing your newsgroups

For example, I add a newsgroup named *local.news* on an INN server running on my Linux system by using the instructions explained in the previous sections. Then I start a newsgreader and set up a new news account with the news server set to my INN server. Then, I access the *local.news* newsgroup. Try it! I bet you'll like it.

![](bbox=[0.85, 0.48, 0.95, 0.67])