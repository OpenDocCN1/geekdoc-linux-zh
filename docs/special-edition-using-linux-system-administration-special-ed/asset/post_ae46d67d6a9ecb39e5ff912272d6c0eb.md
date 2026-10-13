
A fourth special value is possible (x), which indicates that articles that are cross-posted should be removed even if they are still listed in groups which have not expired the article yet.

- The keep field indicates the minimum length of time in days an article should remain in the group.
- The default field indicates the default time in days an article should remain in the group when the article does not provide an Expires header with an alternate expire time.
- The purge field indicates the maximum time in days an article should remain in the group regardless of any alternate expire time specified with an Expires header.

Keep in mind that you are using the CNFS storage method, the expire time is effectively automatic because the size of groups is limited by the size of pre-existing buffer files. In this case, only the /remember/ entry is used from the expires.ctl file. Instead, the entries in the storage.conf file control the expire time of articles in the CNFS storage method as outlined earlier in the section, “Editing storage.conf for CNFS and timehash.”

## CREATING AN ARTICLE SPOOL FOR CNFS STORAGE

If you are using the CNFS storage method, you can create the article spool as follows:

1. For each cycbuff you need to create a buffer file. This can be done using the dd command. For example to create the cycbuffs we have mentioned in our example cycbuff.conf file we need to do the following:

   ```
   # dd if=/dev/zero of=/disk1/cycbuffs/one bs=1k count=2048000
   # dd if=/dev/zero of=/disk1/cycbuffs/two bs=1k count=2048000
   # dd if=/dev/zero of=/disk2/cycbuffs/three bs=1k count=2048000
   # dd if=/dev/zero of=/disk2/cycbuffs/four bs=1k count=2048000
   # dd if=/dev/zero of=/disk3/cycbuffs/five bs=1k count=2048000
   # dd if=/dev/zero of=/disk3/cycbuffs/six bs=1k count=2048000
   # chmod 0644 /disk1/cycbuffs/one
   # chmod 0644 /disk1/cycbuffs/two
   # chmod 0644 /disk2/cycbuffs/three
   # chmod 0644 /disk2/cycbuffs/four
   # chmod 0644 /disk3/cycbuffs/five
   # chmod 0644 /disk3/cycbuffs/six
   ```

2. Each dd command creates a file of the size specified in the count argument filled with zeros. The chmod commands ensure the cycbuffs have the necessary permissions.

## CREATING NEWS HISTORY DATABASE FILES

To build the news history database, you need two files—the newsgroups file, and the active file. The makehistory command uses these files to create the initial history database. The various steps involved to create the history database are described here:

1. Obtain the newsgroup and active files. If you don’t have them with your distribution of INN, download them from ftp.isc.org:/pub/usenet/CONFIG and save them in the db subdirectory of the news user’s home directory (~news/db).
2. Become the news user using the command `su news`.
3. Change to the db subdirectory:

   ```
   $ cd ~/news
   ```

4. Create new history files for your news spool with the following command:

   ```
   $ makehistory -I
   ```

5. This command creates two files: `history.n.dir` and `history.n.pag`.
6. Rename `history.n.dir` to `history.dir`:

   ```
   $ mv history.n.dir history.dir
   ```

7. Rename `history.n.pag` to `history.pag`:

   ```
   $ mv history.n.pag history.pag
   ```

8. Set the permissions on all files in the db directory:

   ```
   $ chmod 644 *
   ```

## SPECIFYING SITES TO FEED TO WITH THE nntpsend.ctl FILE

The nntpsend.ctl file specifies the site that feeds from your server. The file is read by the nntpsend process and consists of a series of entries, one per line. Each entry consists of four colon-separated fields:

```
<site>:<domain name>:<maximum size>:<arguments>
```

The fields are used as follows:

- The site field indicates the name used in the newsfeeds file for this site. The name is used to create a batch file for the feed.
- The domain name field is the fully qualified domain name of the site receiving the feed and the name is passed as an argument to the innxmit process.
- The maximum size indicates the size limit for a batch file. The file will be truncated at this size.
- The arguments are other optional arguments to be passed to the innxmit process.

For example, consider the following entry from an nntpsend.ctl file:

```
news-feed.netvision.net.il:news.netvision.net.il:4m:T800 :t300
```

This entry indicates that articles should be sent to the host news-feed.netvision.net.il and that the batch file should be named news-feed.netvision.net.il. The fully qualified domain name of the site is specified in the next field (news.netvision.net.il). The maximum size field indicates that the maximum batch file size is four megabytes. The final field indicates the arguments to pass to innxmit.

To ensure orderly, regular sending of articles to feed recipients, you must invoke nntpsend from the cron daemon. To do this, create a cron entry similar to the following in the news user's crontab file as outlined in Chapter 7.

```
0,10,20,30,40,50 * * * * /usr/local/news/bin/nntpsend
```

This crontab entry causes nntpsend to run every 10 minutes and send out posted articles which have been queued for transmission.

### Controlling Daily Maintenance with the `news.daily` Script

INN needs to perform daily server maintenance tasks such as expiring old articles and rotating log files. For this to happen you need to create a cron entry for `news.daily` as follows:

```
0 3 * * * /usr/local/news/bin/news.daily expireover lowmark
```

Create this entry in the news user’s crontab file. The entry will cause `news.daily` to run every day at 3 a.m. to perform daily maintenance tasks such as the expire time of articles. Article expire time can be an intensive process and, accordingly, should be run at low usage, off-peak hours.

The `news.daily` script creates a summary report when it runs which is mailed to the news administrator. The report includes disk usage information, log file sizes, the number of entries in the log, incoming article and newsgroups statistics, article expire data, and post-expire data.

### Starting INN at Boot Time with `rc.news`

Generally, you will want to start INN at boot time. Some Linux distributions that include INN will already be configured to do this. If not, you can configure your system to do so by adding the following command to the end of your `/etc/rc.d/rc.local` file:

```
su news -c /usr/local/news/bin/rc.news
```

### Understanding INN Log Files

INN records its activities in the `/usr/local/news/log/news` file. Entry in the file takes the following format:

```
<date> <time> +<feed> <message ID> <site>
```

Optionally, two fields may appear after the message ID field depending on the configuration in the `inn.conf` file:

```
<date> <time> <status> <feed> <message ID> <host name> <size> <site>
```

The feed field indicates the site that sent the article. The message ID field is the article’s ID.

The critical field is the status field. This field can take several possible values as outlined in Table 26.3.

**Table 26.3 — Status in the INN Log File**

| Value | Description |
|---|---|
| `+` | Article was accepted. |
| `j` | Article was accepted but filed in the junk newsgroup. |
| `c` | A cancel message was accepted before the original article arrived; the article is accepted. |
| `-` | Article was rejected. |

If the article is accepted then the site field contains a site-separated list of sites where the article will be sent.

## OTHER LOG FILES

INN generates several other log files, including the following:

- **`expire.log`**: Logs article expiration activities.
- **`innfeed.log`**: Generated if you use innfeed instead of nntpsend.
- **`innfeed.status`**: Logs innfeed connections.
- **`nntpsend.log`**: Logs start and stop times of outgoing connections with nntpsend.
- **`unwanted.log`**: Logs unwanted newsgroups that have been offered.

INN also generates entries logged through the system log facility, syslog. To configure where syslog will store news-related logfiles, edit `/etc/syslog.conf` file.

## ADMINISTERING INN

INN comes with a tool called `ctlinnd` for managing the innd daemon. `ctlinnd` sends messages to the control channel of innd requesting action. innd performs the requested action and sends a message back to `ctlinnd`.

Common ctlinnd commands include those outlined in Table 26.4.

**Table 26.4 — Common ctlinnd Commands**

| Command | Description |
|---|---|
| `ctlinnd mode` | Checks the current mode of the server. |
| `ctlinnd shutdown reason` | Shuts down the server and records the reason in the news log file. |
| `ctlinnd pause reason` | Pauses the server and records the reason in the news log file. |
| `ctlinnd reload all reason` | Forces the server to reload all its configuration files. |
