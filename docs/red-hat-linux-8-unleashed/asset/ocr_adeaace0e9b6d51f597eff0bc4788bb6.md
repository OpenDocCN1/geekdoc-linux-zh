# Filtering Spam with the cleanfeed Package

One problem that has plagued the Usenet newsgroup system is the proliferation of spam email messages. Spam providers often attempt to post their messages to newsgroups to force messages to a large audience. One of the most effective methods for blocking spam messages from being posted to a newsgroup is to use the cleanfeed package. The cleanfeed package is a Perl script that filters out spam before it hits your server. You can configure this software by editing its configuration file, cleanfeed.conf, using the /etc/news directory.

The newsgroup example offered in this chapter is designed for a closed system and doesn't need to filter spam. You can learn more about cleanfeed in the FAQ found at http://www.109.com/~jeremy/news/cleanfeed/

# Newsreaders

Whether or not your Red Hat server is set up as a news server, you can use a newsreader program to read newsgroup articles. The newsreader programs just require a connection to a news server. It doesn't matter if the news server is on the same machine or a remote news server on the other side of the world.

Several programs are available for UNIX systems to connect to news servers to read and post articles in newsgroups. The following describe the newsreaders that are available with the Red Hat Linux distribution.

# The s1rn News Client

The s1rn program is a text-based newsreader program that is included with the Red Hat distribution. It uses the ncurses package to paint text-based windows on the terminal screen. s1rn can be used to read and post articles to newsgroups on a configured news server.

The s1rn program is included in the s1rn RPM package and can be installed by using the rpm command. After you have installed s1rn, your single configuration task is to create an environment variable called NNTPSERVER that points to the news server from which you want to retrieve articles. To locate this variable, the program looks for a file named ~/.jnewsrc. You can use any editor to create this file, but be sure to include it in the value of the environment variable. You should enter something similar to the following in the:

```
NNTPSERVER=maximumhoyt.com
```

When the s1rn program starts, it displays a list of the groups that are available on the news server. You can select which group you want to read articles from and then select the individual articles to read. Figure 20.1 shows a sample s1rn screen.

![](bbox=[0.923, 0.804, 0.979, 0.856])