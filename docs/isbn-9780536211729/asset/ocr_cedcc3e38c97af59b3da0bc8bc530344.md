# Detecting Defaced Web Pages Automatically

The solution is to monitor your site's Web pages yourself. This is easier than sounds and small sites can set this in an hour or two. For highest security, it is recommended that the system is used to monitor the Web site on a completely separate network using a different ISP. This is to detect intrusions that intercept your site upstream from the Web server. For example, this will detect a DNS attack where the cracker lasts your DNS information or how he attacks your ISP. If your monitoring system is inside your firewall using your DNS servers, you will not detect these problems. For medium and large sites, the slight extra cost is worth the security.

I created the tcpread.c program to do the hard part of reading a specified Web page. It is available from the CD-ROM. It can output the page to standard out enable you to make a “reference” snapshot or allow you to do your own “diff” to compare the page to what is expected. Alternatively, it will do the “diff” itself and return a 0 status if it successfully read the page and matched. It will return other exit codes for the different failures. By default, it will read from TCP port 80 and will timeout and return an error if it does not complete the download within 60 seconds. It accounts for the date field varying and handle binaries as well, as images and sound files.

In its simplest usage, it expects the Web server's host name and the page to download. This page name is what you would supply to a browser, starting with the slash that follows the host name. It accepts an optional third argument to specify how many seconds the entry download is allowed to take, rather than the default of 60 seconds. If the site is too slow, tcpread will generate an error that you can detect. This prevents tcpread from hanging. This allows you to detect DoS attacks that slow your system to an unacceptable level. The optional fourth argument is the number to use, rather than the standard 80.

To use this program, it is necessary to generate a list of files to watch. Let us assume that the root of the Apache document tree is /http/htdocs on the Web server and that the monitoring root of the correct_file tree is watch. On the Web server, issue these commands; root permission will not be necessary. The script wwwgenlist may be invoked; it is on the CD-ROM.

```
#!/bin/bash -f
cd /http/htdocs
find -type d -name -print \n  | sed 's/^\.//' > $HOME/m_dirs
# Find and strip leading \.\"
find -type f -print | sed 's/^\.//' > $HOME/m_files"
```