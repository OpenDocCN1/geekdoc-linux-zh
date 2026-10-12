program to authenticate the remote connection and handle the newsreader requests. If the incoming articles are control articles, they are passed to the controlchan program for processing.

Fedora Core has thoughtfully configured the SystemV files that are necessary for starting the news server; you can use (in an appropriate way) chkconfig, ntysysv, service, or system-config-services to start the server. (See Chapter 14, “Automating Tasks,” for details.) Here is an example:

```
# /sbin/service inn start
```

When the innd program is running, you can control it by using the ctlinnd program, with the following syntax:

```
ctlinnd [ -h ] [ -s ] [ -t timeout ] command [ argument...] 
```

The -s option suppresses any output from the ctlinnd command. This option is often used in batch programs. The -t option specifies how long to wait for a response from the server (in seconds). If you are connecting to a server across a slow link or are connecting to a slow server, you can increase the value of timeout.

The command parameters define which actions the ctlinnd program should take with the innd news server. The -h option prints a summary of all the available command parameters that can be used with ctlinnd. For now, you can use the newgroup command to create a new local newsgroup that newsreaders can use to read and send messages:

```
$ ctlinnd newgroup local.linux.group y hoyt@maximumhoyt.com
```

The newgroup command uses three parameters:

+   * The name of the new newsgroup
+   * A flag to define which type of newsgroup to create (y stands for a regular open group and m stands for a moderated group)
+   * An email address for the maintainer of the new newsgroup

The ctlinnd program should be run from the news user ID. If the command is successful, it returns a simple OK message. You can use the ctlinnd command to check whether the new newsgroup has been added to the news server.

# Filtering Spam with the cleanfeed Package

One problem that has plagued the Usenet newsgroup system is the proliferation of spam Usenet messages. Spam providers often attempt to post their messages to newsgroups to force messages to a large, captive audience. One of the most effective methods for blocking spam messages from being posted to a newsgroup is to use the cleanfeed package. The cleanfeed package is a Perl script that filters out spam before it hits your news server. You can configure this software by editing its configuration file, cleanfeed.conf, under the /etc/news directory.