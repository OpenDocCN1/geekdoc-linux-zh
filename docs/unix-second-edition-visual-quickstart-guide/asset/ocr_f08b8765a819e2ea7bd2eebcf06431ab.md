# Downloading the Web with wget

The wget utility allows you to download Web pages—and whole Web sites—to use offline. You just specify a URL and how many levels (links away from the starting page) you want to download, and let wget do its thing (as in Code Listing 12.4). Then you can use the Web pages when you’re not connected to the Internet, like while on an airplane, in a hotel, or in a waiting room, for example.

# To download the Web with wget:

+   1. wget http://www.cnn.com/
+      At the shell prompt, type wget followed by the URL of a Web site or FTP site. Here, we’re accessing the CNN Web site (Code Listing 12.4).
+   2. Slurp!
+      Hope you had plenty of space.
+   3. links index.html
+      Then use your favorite Web browser to check out your handiwork.

# ✓ Tips

+   - We recommend using a separate directory to contain the contents of different Web sites. Otherwise, wget will either rename files to avoid clobbering existing files (thus breaking links) or clobber existing files (thus making it highly likely that only the last Web site you downloaded will be complete. If you use wget with the -x option (as in, wget -x http://www.example.com/), it’ll do this automatically. See Chapter 2 for more on using directories.

```
jdoe /home/jdoe $ wget http://www.cnn.com/
--18:07:51--  http://www.cnn.com/
=> `index.html'
Resolving www.cnn.com... done.
Connecting to www.cnn.com[64.236.24.4]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]

[ <=> ] 51,29053.28K/s

18:07:53 (53.28 KB/s) - `index.html' saved
[51290]
jdoe /home/jdoe $
```

Code Listing 12.4 You can use wget to download as much of the Web as you can handle.

+   - wget --recursive --level=2 http://www.example.com/ lets you get several (two, in this case) levels of a Web site. Be careful, because it’s easy to bite off more than you can chew. We ended up with more than 20 MB from this command on www.cnn.com.
+   - wget also works for FTP sites. Just use wget ftp://ftp.example.com or wget jdoe:iAsecret@ftp.example.com if you need to specify a password.
+   - Check out the man page for wget (man wget) for more on the extensive options available.