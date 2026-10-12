retrieve_one is useful for purposes such as ordering a current copy of a FAQ into your local directory; start experimenting with it by making a request with the following:

```
# retrieve_one rtfm.mit.edu:/pub/usenet-by-hierarchy/comp/os/linux/answers/linux/info-sheet
```

Red Hat Linux comes with other utilities you can use for FTP retrieval. See Chapter 11, “FTP,” for information about the ncftp and gftp commands.

# HTTP Retrieval

For an HTTP interaction, let the Lynx browser do the bulk of the work. The Lynx browser that accompanies the Red Hat distribution is adequate for all but the most specialized purposes. You can obtain the latest version at http://lynx.browser.org. Although most Lynx users think of Lynx as an interactive browser, it’s also handy for dropping a copy of the latest headlines, with live links, in a friend’s mailbox with this:

```
# lynx -source http://www.cnn.com | mail someone@somewhere.com
```

To create a primitive news update service, script the following and launch it in the background (using the ampersand, &):

```
NEW=/tmp/news.new
OLD=/tmp/news.old
URL=http://www.cnn.com
while true
do
mv SNEW SOLD
lynx -dump -nolist $URL >$NEW
diff SNEW SOLD
# Wait ten minutes before starting the next comparison.
sleep 600
done
```

Any changes in the appearance of CNN’s home page will appear onscreen every 10 minutes. This simple approach is less practical than you might first expect because CNN periodically shuffles the content without changing the information. It’s an instructive example, however, and a starting point from which you can elaborate your own scripts.

# Conclusions on Shell Programming

Shells are glue; if there’s a way to get an application to perform an action from the command line, there’s almost certainly a way to wrap it in a shell script that gives you power over argument validation, iteration, and input-output redirection. These are powerful techniques and well worth the few minutes of study and practice it takes to begin learning them.