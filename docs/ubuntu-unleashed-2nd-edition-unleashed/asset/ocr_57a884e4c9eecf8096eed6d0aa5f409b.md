```
13:13:28 (632.81 KB/s) - `.listing` saved [648]

Removed `.listing`.
--13:13:28--  ftp://phudson:*password*@stinky/mp3/C31821-01A.mp3
    => `C31821-01A.mp3`

==>
CWD not required.
==>
PORT ... done.  ==> RETR C31821-01A.mp3 ... done.
Length: 5,172,089

60% [====================>          ] 3,123,680  264.80K/s  ETA 00:07
```

In this example, the user retrieves all files in a directory named mp3 (under /home/paul) on the remote host named stinky. The wget command will first retrieve a directory listing, then proceed to download the specified files (all marked with `*` in this example). Note that you can specify a username and password (mypassword in the example) on the command. This generally is not a good idea. It is better, but still not really secure, approach is to save the password in a file named .wgetrc in your home directory. See the wget man page for more information, or check the only documentation at http://www.gnu.org/software/wget/manual/wget-1.8.1/html_mono/wget.html.

# TIP

Another popular use for wget is downloading complete copies of websites for offline reading, although it is not very friendly toward website owners who have to pay for all the bandwidth!

To download an entire site, you need to specify the --mirror, --convert-links, and -p parameters, followed by the URL of the site to download. The first parameter tells wget to download all the pages and pictures from the site, following links as it can. The second tells it to rewrite the HTML so that it works when browsed locally. The last parameter, -p, tells wget to download all the files referenced in the HTML, such as sounds, CSS files, and other related documents. You might also want to specify the -w parameter, which allows you to specify a number of seconds between individual wget requests; this stops your download from overloading the web server.
So, the complete command to download a website would be wget --mirror --convert-links -p -w 2 http://www.example.com/.

# Using Graphical FTP Clients

Many graphical FTP clients are available for Linux. Ubuntu includes the graphical gFTP client (in the gftp-gtk package) and network-aware browsers included with GNOME and KDE. These browsers feature built-in drag-and-drop capability, thus ensuring FTP functionality. Other graphical interface clients that can be used for FTP include the Firefox web browser (the FireFTP extensive is particularly good), KDE's Konqueror, GNOME's Epiphany, and the Nautilus file manager.