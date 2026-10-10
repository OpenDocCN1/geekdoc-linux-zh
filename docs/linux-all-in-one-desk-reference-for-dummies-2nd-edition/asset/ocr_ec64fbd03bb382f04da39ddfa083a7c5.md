Table 4-2 (continued)
| Parameter Name | Description |
| --- | --- |
| pathhost | Set this parameter to the name of your news server as you want it to appear in the Path header of all postings that go through your server. If pathhost isn't defined, the fully qualified domain name of your system is used. |
| pathnews | Set this parameter to the full pathname of the directory that contains INN binaries and libraries. The default pathnews is set to /usr/lib/news. |
| domain | Set this parameter to the domain name for your server. |
| allownewnews | Set this parameter to true if you want INN to support the NEWNEWS command from newsreaders. In the past, this option was set to false because the NEWNEWS command used to reduce the server's performance, but nowadays the default is set to true because modern servers can easily handle the NEWNEWS command. |
| hiscachesize | Set this parameter to the size in kilobytes that you want INN to use for caching recently received message IDs that are kept in memory to speed history lookups. This cache is used only for incoming feeds, and a small cache can hold quite a few history file entries. The default setting of 0 disables history caching. If you have more than one incoming feed, you may want to set this parameter to a value of 256 (for 256KB). |
| innflags | Set this parameter to any flags you want to pass to the INN server process when it starts up. |

# The newfeeds file

The newfeeds file specifies how incoming news articles are redistributed to other servers and to INN processes. If you provide news feeds to other servers, you have to list these news feeds in this file. (You also must have an entry labeled *ME*, which serves a special purpose that I explain later in this section.)

The newfeeds file contains a series of entries, one for each feed. Each feed entry has the following format:

```
site(/exclude,exclude,. . . )\
  :pattern, pattern. . .{ /distrib, distrib. . .}\
  :flag, flag. . .
  :param
```