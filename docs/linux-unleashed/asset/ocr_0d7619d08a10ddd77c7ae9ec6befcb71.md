processes arriving articles. However, it does take system resources away. To set `nthreads` in daemon mode, use the `-d` option. By default, `nthreads` will check the newsgroups every 10 minutes. You can place this command in the `rc` startup files, if you want.

# # Configuring tin

Unlike `trn`, the `tin` newsreader doesn't need to be told to reindex the thread databases at intervals. The `tin` newsreader generates the thread indexes every time a user enters a newsgroup. The reindexing is quite fast, unless the newsgroup has more than 500 articles or so.

When `tin` reindexes a newsgroup, it stores the index file under the user's home directory as `.tin/index/newsgroup_name`. The total size of all these index files can become quite sizable if a user reads a lot of newsgroups or if there are many users on the system. The easy way to prevent this is to force `tin` to keep a single master index in one location that all users can access. To set up a single index, set the owner of `tin` to news with the command

```
chown news.news tin
```

(when you are in the `tin` directory, of course). This way, `tin` stores the index files under `/usr/spool/news/.index` (or `/var/spool/news/.index`).

You can install a daemon called `tind` that keeps the index files constantly updated. The `tind` daemon source code is supplied with some versions of Linux, but few have a compiled version, so you will need a compiler and the `make` utility to build a version for your system.

# # Summary

Once you have completed the compilation and configuration of the NNTP system, as well as your newsreaders, you're set to go. There are quite a few new newsreaders appearing for Linux, such as `nn`, which is also a threaded newsreader. The choice of a reader is a matter of personal preference. Experiment and find the one you want to use.

From here, there are a number of related chapters that may be of interest to you. To learn how to

+   - Secure your network from hackers, read Chapter 42, "Network Security."
- Back up all the configured software you've installed, read Chapter 45, "Backups."
- Automate tasks like downloading news at night, read Chapter 46, "cron and at."