```
FTP_PATH=/debian/dists/lenny/main/installer-i386/current/images/cdrom
REMOTE_FILE=debian-cd_info.tar.gz

ftp -n << _EOF_
    open $FTP_SERVER
    user anonymous me@linuxbox
    cd $FTP_PATH
    hash
    get $REMOTE_FILE
    bye
_EOF_

ls -l $REMOTE_FILE
```

# Summing Up

In this chapter, we started a project that will carry us through the process of building a successful script. We introduced the concept of variables and constants and how they can be employed. They are the first of many applications we will find for parameter expansion. We also looked at how to produce output from our script, and various methods for embedding blocks of text.

# Further Reading

+   - For more information about HTML, see the following articles and tutorials:
+     http://en.wikipedia.org/wiki/Html
+     http://en.wikibooks.org/wiki/HTML_Programming
+     http://html.net/tutorials/html/
+   - The bash man page includes a section entitled "HERE DOCUMENTS," which has a full description of this feature.