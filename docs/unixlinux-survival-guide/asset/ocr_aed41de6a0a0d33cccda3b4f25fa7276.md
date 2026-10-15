```
</item>
</channel>
</rss>
```

The file shown in Listing 6.24 uses another feature from the specification. The URL in the <link> tags points to a Web address containing the elaborate details concerning the news item. Most News Readers open this URL as answer to a double-click on the item. The structure of the file is not that complicated, but maintaining it by hand is error-prone and puts an unnecessary strain on the maintainer of the news. To automate the process somewhat, you could use the script shown in Listing 6.25.

# LISTING 6.25 Script for Generating the RSS File

```
#!/usr/bin/sh
# $Id: genrss1.sh,v 1.2 2004/09/13 11:31:46 erikk Exp erikk $
########################################################
#
#    file:         genrss1.sh
#    purpose:      generates an rss 2.0 feed from
#                  the files stored in the directory
#                  articles
#    author:       Erik Keller
#    parameters:   none
########################################################

# Variables
WORKDIR=/export/home/users/erikk/work/newstick
ARTICLEDIR=$WORKDIR/articles
RSSFILENAME=$WORKDIR/internalnews.rss

# create the header
echo "<rss version=\"2.0\">" > $RSSFILENAME
echo "<channel>" >> $RSSFILENAME
echo "<title>example.domain internal news</title>" >> $RSSFILENAME
echo "<link>http://internalweb.example.domain</link>" >> $RSSFILENAME
echo "<description>example.domain internal newswire</description>" >> $RSSFILENAME
echo "<language>en</language>" >> $RSSFILENAME
```