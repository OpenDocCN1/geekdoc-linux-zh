# Introduction to trn

There are many newsreaders available for Linux systems, but trn remains the perennial favorite. This is an old package but is simple to use as well as fast and efficient. You might not need a newsreader at all if you have Web services on your system. Many Web browsers allow access to newsgroups either in your own news directory or through a connection to an ISP’s newsfeed.

The primary advantage of trn over the earlier rn (read news) package is that trn lets you follow threads. A thread in a newsgroup is a continuing discussion with one primary subject. Before trn came along, you had to read news consecutively from first to last, trying to assemble several different conversations into logical groups as you went. When trn became available, you could start with one thread, read all the postings about that subject, and then move on to another subject, regardless of the chronological order in which the postings were made.

Threads are usually handled automatically without requiring any special user interaction, although there is some work performed behind the scenes on your newsfeed. Some newsgroups do not support threading, but most do. If threads are available, you can follow the thread from start to finish, or jump out and change threads at any time.

# Installing and Configuring trn

The trn newsreader is easy to install as a binary package; an RPM is included with Red Hat Linux. Type the following to see if trn is already installed on your system:

```
```bash
rpm -q trn
```
```

If no package by that name is found, you can install the trn package from the directory containing RPM files by issuing the following command:

```
```bash
rpm -i trn-3.6-25.i386.rpm
```
```

There really is no special configuration required for trn to run. When the binary is available on your system, it will check for the newsgroup information in /var/lib/news and present it to you. In the past, trn wasn’t capable of forming threads on its own. Because of this, external threading utilities such as threads or override were once popular. As of version 3.0, however, trn supports direct threading without the need for external thread utilities. Most users now use trn as a standalone program.