In this example, we have also told rsync to use ssh to connect to the server. We do have an rsync server that can be used, but most people just use ssh to transport data because many servers are running rsync and not the rsync server.

In the example, when specifying the server (www.palmcoder.net), we specially identified the directory to copy over, separated by a colon (:). As we have not put a forward slash (/) at the end of the blog directory, rsync copies the directory and its contents to our local machine. If a forward slash was added to the directory specified, we would only copy the contents of the directory and not the directory itself. Be wary about this because it is easy to copy everything except expecting if you miss a forward slash.

If you want to make sure any files that were deleted from the originating server were actually deleted on the local machine when synchronized, you need to add the -delete parameter to the command-line options.

# # wget

If you need to download web pages or files from FTP quickly, you can use wget. It's a great tool if you need to get a file onto a server when you do not have a web browser, which is very common.

The wget command is used only to transfer files over HTTP and FTP. It is not to be confused with something like rsync, which is a general network copy system.

In its simplest form, all you have to pass is the URL you want to download to the wget command (see Listing 15-14). This downloads the URL specified to the local directory.

> Downloading a File over HTTP to Your Local Server

```
bible:- # www.palmcoder.net/index.php
--03:26:23 - http://www.palmcoder.net/index.php
-- "index.php"
Resolving www.palmcoder.net...212.13.208.115
Connecting to www.palmcoder.net [212.13.208.115]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
OK ........ 59.59 KB/s
03:26:23 (59.59 KB/s) - 'index.php' saved [8608]
```