# **TABLE 29.1** Continued

| Program File | Description |
| :--- | :--- |
| mailpost | Manually sends a mail message into a specified newsgroup |
| **makeindex** | Creates binary indexed database files from the history file |
| **maketext** | Creates a text history file of message IDs seen by the news server |
| **nnexpdaily** | Runs as a cron job to perform daily maintenance on the news server |
| nntp | Communicates with newsreaders via the nntp daemon |
| nntpgt | Connects to a remote news server and retrieves articles that are specified on the standard input |
| nntpsend | Connects to a remote news server and posts articles to newsgroups |
| ovdb_recover | Attempts to repair a damaged INN database file |
| ovdb_upgrade | Attempts to upgrade an existing INN database file |
| **qrimination** | Removes specific filenames from the history file |
| **rmlnews** | Retrieves newsgroup articles from one news server and forwards them to another news server |
| rnews | Receives newsgroup articles from a news server by using a UUCP connection |
| scanlogs | Summarizes information in the INN log files and performs general cleaning and rotating of the log files |
| tin | Provides a command-line interface to the article storage manager |

As you can see in Table 29.1, a number of the INN programs are used to help facilitate the news process on the server. The INN package also contains a number of configuration files that define how articles are handled. Table 29.2 lists and describes these files.

# **TABLE 29.2** INN Package Configuration Files

| Configuration File | Description |
| :--- | :--- |
| control.ctl | Specifies how control messages are handled |
| expire.ctl | Specifies how articles are expired |
| incoming.conf | Specifies addresses and authentication information for servers that send newsfeeds to your news server |
| inn.conf | Acts as the primary general configuration file for the innd program |
| innfeed.conf | Specifies parameters for the incoming newsfeed handler |
| innwatch.ctl | Determines how the innwatch program monitors the INN system |
| moderators | Specifies email addresses for moderators of moderated newsgroups |
| modt.news | Specifies which information is posted to newsreaders when a list modt command is sent |
| newsfeeds | Specifies which newsgroups are fed to other news servers from this news server |
| nnrpd.track | Specifies newsreaders or servers that should have their activity recorded during an NNTP session |
| nntpsend.ctl | Specifies remote news servers that your news server feeds articles to in batch mode |
| passwd.nttp | Specifies passwords used to connect to remote news servers |