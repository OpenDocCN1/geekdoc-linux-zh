+   ♦ xyz.wanted — Wanted (help, items to buy, and so on) postings by employees
+   ♦ xyz.technical.hardware — Technical discussions about hardware
+   ♦ xyz.technical.software — Technical discussions about software

# Updating configuration files

Here are the steps you follow to update the configuration files for your local newsgroups and then restart the news server:

1. Add descriptive entries for each of these newsgroups to the /var/lib/news/newsgroups file.

Here are the entries from the default /var/lib/news/newsgroups file:

```
control          Various control messages (no posting).
control.cancel   Cancel messages (no posting).
control.checkgroups  Hierarchy check control messages (no posting).
control.newgroup Newsgroup creation control messages (no posting).
control.rmgroup  Newsgroup removal control messages (no posting).
junk             Unfiled articles (no posting).
```

Add to this file a line for each local newsgroup — type its name, followed by a brief description. For example, here's what you might add for the xyz.general newsgroup:

```
xyz.general   General items about XYZ Corporation
```

2. Edit the ME entry in the /etc/news/newsfeeds file and add the phrase !xyz.* to the comma-separated list of newsgroup patterns.

This ensures that your local newsgroups are not distributed outside your site.

3. Add a storage method to be used for the local newsgroups.

For example, you can add the following lines in /etc/news/storage.conf to define the storage method for the new xyz hierarchy of newsgroups (change xyz to whatever you name your local newsgroups):

```
method tradspool {
    class: 1
    newsgroups: xyz.*
}
```

4. To make these changes effective, restart the news server with the command:

```
service inn restart
```