# **Try It Out**  Compiling the gFTP Application

+   1. First, you must determine the root source directory where we will be building *any* and *all* applications. A good directory to choose is `/usr/local/src`, since it is separate from the standard operating system installation directories. Remember, you need to be logged on as the root user to have the necessary privileges to create and modify files in this directory.

+   2. Once you have decided on the root source directory, you should create a subdirectory where you will unpack the source code for the application. Some source code packages when unpacked will create a directory to hold all of their files, while others will irresponsibly dump the files into the current directory. We take this step to ensure that we do not end up with source code files cluttered all over the `/usr/local/src` root directory.

```
`# mkdir /usr/local/src/gftp`
```

+   3. Now, you can go ahead and obtain the source code for gFTP from the following URL:
+   
+       http://www.gftp.org/gftp-2.0.14.tar.gz
+   
+       Notice that the source code is distributed as a compressed tar archive. You can download it using a Web browser, or by using the wget program, like so:

```
# cd /usr/local/src/gftp
# wget http://www.gftp.org/gftp-2.0.14.tar.gz
--19:07:51--  http://www.gftp.org/gftp-2.0.14.tar.gz
=> 'gftp-2.0.14.tar.gz'
Resolving www.gftp.org... done.
Connecting to www.gftp.org[18.244.0.188]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1,136,930 [application/x-tar]

100%[===================================================>] 1,136,930 28.47K/s  ETA 00:00
19:08:30 (28.47 KB/s) - 'gftp-2.0.14.tar.gz' saved [1136930/1136930]
```

+   4. The next step is to uncompress and untar the archive:

```
# tar -zckvf gftp-2.0.14.tar.gz
gftp-2.0.14/
gftp-2.0.14/config.h.in
gftp-2.0.14/COPYING
gftp-2.0.14/Makefile.am
...
gftp-2.0.14/README
gftp-2.0.14/gftp.spec
```