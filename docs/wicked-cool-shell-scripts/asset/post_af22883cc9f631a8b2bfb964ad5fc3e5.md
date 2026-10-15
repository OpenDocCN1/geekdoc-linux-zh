
## 7
## WEB AND INTERNET USERS

![](img/4ffb1cc24a1b24b49254839643abedb2_204_0.png)

One area where Unix really shines is the internet. Whether you want to run a fast server from under your desk or simply surf the web intelligently and efficiently, there’s little you can’t embed in a shell script when it comes to internet interaction.

Internet tools are scriptable, even though you might never have thought of them that way. For example, FTP, a program that is perpetually trapped in debug mode, can be scripted in some very interesting ways, as is explored in Script #53 on page 174. Shell scripting can often improve the performance and output of most command line utilities that work with some facet of the internet.

The first edition of this book assured readers that the best tool in the internet scripter’s toolbox was lynx; now we recommend using curl instead. Both tools offer a text-only interface to the web, but while lynx tries to offer a browser-like experience, curl is designed specifically for scripts, dumping out the raw HTML source of any page you’d like to examine.

For example, the following shows the top seven lines of the source from the home page of Dave on Film, courtesy of curl:

```
```bash
$ curl -s https://www.daveonfilm.com/ | head -7
<!DOCTYPE html>
<html lang="en-US">
<head>
<meta charset="UTF-8" />
<link rel="profile" href="http://gmpg.org/xfn/11" />
<link rel="pingback" href="http://www.daveonfilm.com/xmlrpc.php" />
<title>Dave on Film: Smart Movie Reviews from Dave Taylor</title>
```
```

You can accomplish the same result with lynx if curl isn’t available, but if you have both, we recommend curl. That’s what we’ll work with in this chapter.

> One limitation to the website scraper scripts in this chapter is that the script depends on a website that’s changed its layout or API in the time since the book was written, the script might be broken. But if you can fix HTML or JSON (even if you don’t understand it all), you should be able to read any of these scripts. The problem of tracking other sites is exactly why Extensible Markup Language (XML) was created: it allows site developers to provide the content of a web page separately from the rules for its layout.

### #53 Downloading Files via FTP

One of the original killer apps of the internet was file transfer, and one of the simplest solutions is FTP, File Transfer Protocol. At a fundamental level, all internet interaction is based on file transfer, whether it’s a web browser requesting an HTML document and its accompanying image files, a chat server relaying lines of discussion back and forth, or an email message traveling from one end of the earth to the other.

The original FTP program still lingers on, and while its interface is crude, the program is powerful, capable, and well worth taking advantage of. There are plenty of newer FTP programs around, notably FileZilla (http://filezilla-project.org/) and NcFTP (http://www.ncftp.org/), plus lots of nice graphical interfaces you can add to FTP to make it more user-friendly. With the help of some shell script wrappers, however, FTP does just fine for uploading and downloading files.

For example, a typical use case for FTP is to download files from the internet, which we’ll do with the script in Listing 7-1. Quite often, the files will be located on an anonymous FTP servers and will have URLs similar to ftp://<some server>/<path>/<filename>/.

### The Code

```
#!/bin/bash

# ftpget--Given an ftp-style URL, unwraps it and tries to obtain the
# file using anonymous ftp

anonpass="$LOGNAME@$(hostname)"

if [ $# -ne 1 ] ; then
 echo "Usage: $0 ftp://..." >&2
 exit 1
fi

# Typical URL: ftp://ftp.ncftp.com/unixstuff/q2getty.tar.gz

if [ "$(echo $1 | cut -c1-6)" != "ftp://" ] ; then
 echo "$0: Malformed url. I need it to start with ftp://" >&2
 exit 1
fi

server="$(echo $1 | cut -d/ -f3)"
filename="$(echo $1 | cut -d/ -f4-)"
basefile=$(basename $filename)

echo "$0: Downloading $basefile from server $server

ftp -np << EOF
open $server
user ftp $anonpass
get "$filename" "$basefile"
quit
EOF

if [ $? -eq 0 ] ; then
 ls -l $basefile
fi

exit 0
```

Listing 7.1: The ftpget script

### How It Works

The heart of this script is the sequence of commands fed to the FTP program starting at 1. This illustrates the essence of a batch file: a sequence of instructions that’s fed to a separate program so that the receiving program (in this case FTP) thinks the instructions are being entered by the user. Here we specify the server connection to open, specify the anonymous user
