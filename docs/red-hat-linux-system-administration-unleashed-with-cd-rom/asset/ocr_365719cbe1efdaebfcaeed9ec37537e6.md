Next, you need to create an empty history database. You can do this by running the following command:

```
makehistory -i
```

When it is finished, you need to move history.n* to history.*. Finally, set the file permissions on all of the files you just created:

```
chmod 0664 *
```

Your news database files are now ready to go.

# Setting up the News.Daily cron Job

INN requires a special cron job to be set up on your system to run the news.daily script, which performs daily server maintenance tasks such as article expiration and the processing and rotation of the server logs. Because it will slow the server down while it is running, it should be run during periods of low server usage, such as in the middle of the night. To run it at 3 a.m., for example, add the following entry to the news user's crontab file:

```
0 3 * * * /usr/local/news/bin/news.daily expireover lowmark
```

Also, a cron job should be set up to transmit to your upstream site any articles that have been posted locally and queued for transmission; for example:

```
1,11,21,31,41,51 * * * /usr/local/news/bin/nntpsend
```

The pathnames and user ID are the installation defaults; change them to match your installation if you used something other than the defaults.

The parameters passed to news.daily in the preceding example are the most common (and usually the most efficient) ones to use. More information on what these parameters do can be found in the news.daily man page.

# Starting the System

INN is normally started via the shell script rc.news. This must be run as the news user and not as root. Put the following command (or something similar) into the system boot script:

```
su news -c /usr/local/news/bin/rc.news
```

If innd gets stopped or killed and you want to restart it without rerunning rc.news, run inndstart:

```
/usr/local/news/bin/inndstart
```

If you added any values to the innflags variable in inn.conf, you'll need to add the same values to the command line of inndstart if you run it by hand.