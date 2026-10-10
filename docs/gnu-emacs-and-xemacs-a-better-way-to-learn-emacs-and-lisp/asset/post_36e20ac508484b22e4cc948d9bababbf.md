
include your news server, mail back ends, WWW back ends, and directory groups you have created. Pressing Enter on any of the servers listed takes you to a Group buffer listing available newsgroups, mail folders, or whatever other types groups the server has available. You can subscribe and unsubscribe to any group by pressing u, the toggling key.

The last of the main groups you should be aware of is the zombie group. This is a group that Gnus knows about and can access but to which you haven't subscribed. Many zombie groups are newly available groups from your news server, and others are groups you have accessed in previous sessions but haven't subscribed to. Every now and then, it's a good idea to take a look at your zombies. There might be some to which you would like to subscribe with the u command; the others can be cast out with this command:

```
s z
```

### The Summary Buffer

After you have selected a group, a new type of Gnus buffer is created—the Summary buffer, a list of unread articles or postings. The sender, subject line, and server's message number are shown, one article per line.

If you select your group by pressing the spacebar rather than Enter, the first unread article is shown in another window, as shown in Figure 18.4.

![](img/c8827ea52a0796def3f6891892ed9d3a_388_0.png)

Figure 18.4 Summary and Article Buffers

There are several ways of moving focus from article to article. The up-arrow and down-arrow keys are intuitive, as is clicking the second mouse button, so use these for the time being since there are so many other keystrokes to remember.

Press Enter or the spacebar (or click with the mouse) to fetch an article from the server. It appears in a new Article window, and a capital R to the left of the message's line in the Summary buffer indicates that it has been marked as read.

Often, when reading news posts, you finish reading the messages that interest you and you never want to see the remainder again. Consign them to oblivion by pressing c, which stands for "catch up" (What this really does is mark all messages in the Summary buffer as read. This is recorded in your ~/.newsrc file so that the next time you read news, only new messages in the group are seen. You can also press c on a group listing in the Group buffer, which marks all messages as read without opening the group.)

The window focus never needs to leave the Summary buffer, because article-related commands in a sense "cross the modline" between Summary and Article windows. Page up and down through an article with the spacebar and Delete keys. There is a class of Summary commands that limit the groups displayed by using various filtering criteria. Here are the three most commonly used:

- After you type this command, only articles with the current message's subject are shown.
- `/a` Limits the display so that only articles by the current article's author are shown.
- `/u` Hides the messages already marked as read.

Gnus can display articles arranged in *threads*, which are hierarchical branching trees of articles. Sometimes this is useful, but in some groups, you might want to see all articles in a continuous sequence. You can toggle thread display with this command:

```
T T
```

Over the years, Gnus commands seem to have bred like rabbits. There are quite a few thread-related commands, some of them arcane but presumably used by some advanced Gnus aficionados (although it's amusing to speculate that there might be commands that no one has ever used!). Here are a few thread commands that make a good starting point:

| Command | Description |
| :--- | :--- |
| T s | Fans out or exposes the threaded messages hiding beneath the current article. |
| T h | Collapses the current article's threaded replies, hiding them. |
| T S | Shows all threads. |
| T H | Conceals all threads. |

The Gnus Info manual details the remaining thread commands, but using the mouse to navigate is nearly as fast, and you don't need to learn still more keyboard commands.

## Articles

Once you have an article displayed in its own window, more commands come into play. As mentioned in the preceding section, the spacebar and Delete page back and forth through the message. Several categories of actions can be used on an article, including marking, saving, scoring, and caching (you will find more in the Gnus Info manual).

### Marking or Tagging

Often there will be several articles in a Summary buffer that you would like to treat the same way. Gnus offers a variety of tags you can hang on an article. A marked article's particular tag shows up in the Summary buffer. Here are the most useful of these commands:

| Command | Description |
| :--- | :--- |
| # | The basic processing tag. If you mark several articles with this, a subsequent command is applied to them all. |
| M-# | Untags the current article. |
| M P U | Untags all marked articles. |
| M P t | Tags all articles in the current thread. |
| M P T | Untags articles in the current thread. |
| ? | Makes an article dormant. A dormant article isn't visible in the Summary buffer unless someone has replied to it. This, so to speak, "wakes it up". This command can be used when you have posted a message and you don't want to see it again until there is a response. The article is stored in the disk cache (see the section "The Local Cache"). |
| M-u | Marks the article as unread, even if you have read it. |
| Ctrl-k | Marks all messages with the same subject as read. |
| k | Marks all messages with the same subject as the current one as read and then opens the next message. |
| M-s | Searches for regular expression matches in all articles in the current group. |

As with all of these command categories, you can find many more marking commands on the menus and described in the Gnus Info files.

### Saving Articles

If you follow certain favorite newsgroups, you are likely to happen across articles you would like to keep permanently. These might be wonderful examples of prose, software tips or code snippets, or possibly entire threads in which you participated. You also might be accumulating a collection of encoded image or sound files from one of the binary newsgroups.

Most news servers periodically discard articles when they reach a certain age due to disk space limitations, so you can't count on an article's being available from your server indefinitely. Gnus can save an article in a number of different formats, but if you save very many articles, keeping them organized and identifiable can become time-consuming. Consider using persistent caching (discussed later) if your collection becomes unmanageable. Here are the main article-saving commands:

- `o` Saves the current article to an Rmail (Babyl-format) file. This command appends the article to an Rmail folder. The default filename is the name of the newsgroup, but you can type in something else if you like. This is one way to accumulate an archive of valuable postings from a group. You might want to use this command if Rmail is your mail reader; otherwise, don't use it, because the Babyl format is understood by only Rmail and Gnus.
- `o m` Similar to o, but uses the standard UNIX mailbox format.
- `o f` Appends the entire article to a plain text file.
- `o F` The same as o f, but overwrites the file, destroying the file's contents.
- `o v` Appends the article to a VM-style mail folder. This is useful if you use VM, because you will be able to read the folder from your VM sessions.

Another way to save an article locally but still have it show up in future Summary buffers is to make it persistent. See the section “The Local Cache” for details.

### Scoring

*Scoring* is a newsgreader term for rating or assigning a relative value to an article. The idea is that similar articles in the future, perhaps those with the same subject or author, will inherit a score. Gnus will try to make the article more prominent if the score is high. Articles with a low or negative score won't even appear in the Summary buffer. The default score is a neutral 0.

You may be more familiar with kill files, used by some newsgreader software for a similar purpose. A kill file is a list of patterns which match some combination of subject, author, or other header lines in a message. The newsgreader ignores any message which matches one of these patterns. Gnus can use kill files but they are much slower to parse and less flexible than article scoring. Kill files require more user maintenance while scoring can be automated in various ways.

There are two varieties of scores—persistent and expirable. Persistent scores stay in effect forever unless you deliberately remove them, and expirable scores last for a limited time.

Roughly speaking, persistent scores tend to be used for scoring based on an author's name, because people tend to live on and keep their names. Expirable scores are well-suited for scoring based on a message's subject, because subjects come and go.

Scores are stored in Lisp files, one for each newsgroup. Armed with a basic knowledge of Lisp syntax (which you can glean from some of the earlier chapters), you can directly edit your score files. Sometimes this is faster than figuring out the exact command you need for scoring a message in a particular way, because score command syntax can become convoluted.

To edit the score file for the current group (assuming you are viewing a Summary buffer), press M-x and type

```
gnus-score-mode
```

or use a direct key command:

```
v e
```

The following command loads the current score file into a score-mode buffer for editing:

```
v f
```

You are prompted for the name of another score file, which will be loaded for editing. This file then becomes the current score file.
