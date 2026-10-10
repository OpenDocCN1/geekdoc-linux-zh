# Configuring and Starting the INN Server

Each entry has four fields separated by colons (:). Usually, the entries span multiple lines, and a backslash (\) at the end of the line is used to continue a line to the next. Here’s what the four fields mean:

+   ◆ The first field, site, is the name of the feed. Each name must be unique, and for feeds to other news servers, the name is set to the host name of the remote server. Following the name is an optional slash (/*) and an exclude list (*exclude_*, *exclude_*…), of names. If any of the names in this list appear in the path line of an article, that article isn’t forwarded to the feed. You can use an exclude list if you don’t want to receive articles from a specific source.

+   ◆ The second field is a comma-separated list of newsgroup patterns, such as `*@alt.barnries.warez.*,!control*,!local*`, followed by an optional distribution list. The distribution list is a list of comma-separated keywords, with each keyword specifying a specific set of sites to which the articles are distributed. The newsgroup patterns essentially define a subscription list of sites that receive this news feed. An asterisk (*) matches all newsgroups. A pattern beginning with an ! causes newsgroups matching that pattern to be dropped. A pattern that begins with an exclamation mark (!) means the matching newsgroups are not sent. By the way, the simple pattern-matching syntax used in INN configuration files is referred to as a wildmat pattern.

+   ◆ The third field is a comma-separated list of flags — fields that determine the feed-entry type and set certain parameters for the entry. You see numerous flags; type `man newsfeeds` and read the man page for more information about the flags.

+   ◆ The fourth field is for parameters whose values depend on the settings in the third field. Typically, this field contains names of files or external programs that the INN server uses. You can find more about this field from the newsfeeds man page.

Now that you know the layout of the `/etc/news/newsfeeds` file, you can study that file as an example. The default file contains many sample feed entries, but only two are commented out:

+   ◆ `ME` is a special feed entry that’s always required. It serves two purposes. First, the newsgroup patterns listed in this entry are used as a prefix for all newsgroup patterns in all other entries. Second, the `ME` entry’s distribution list determines what distributions your server accepts from remote sites.

+   ◆ The `controlchan` feed entry is used to set up INN so that an external program is used to handle control messages. (These messages are used to create new newsgroups and remove groups.) For example,

![](bbox=[0.88, 0.53, 0.98, 0.71])