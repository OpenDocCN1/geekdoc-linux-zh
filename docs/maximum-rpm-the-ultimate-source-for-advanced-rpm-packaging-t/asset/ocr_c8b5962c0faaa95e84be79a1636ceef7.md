```
+ cd /usr/src/redhat/BUILD/amanda-2.3.0
+ chown -R root.root .
+ chmod -R a+rX,g-w,o-w .
+ exit 0
#
```

By looking at the output, it would be pretty hard to miss the fact that the sources were un-
packed. If we look in RPM's default build area (\texttt{/usr/src/redhat/BUILD}), we'll see an amanda
directory tree:

```
# cd /usr/src/redhat/BUILD/
# ls -l
total 3
drwxr-xr-x 11 root root 1024 May 19 1996 amanda-2.3.0
#
```

After a quick look around, it seems like the sources were unpacked properly. But wait—where
are our carefully crafted configuration files in \texttt{conf ig}? Why isn't \texttt{tools/munge} modified?

# ### 20.3.4. Getting Patches Properly Applied

Ah, perhaps our \texttt{%prep} script was a bit too simple. We need to apply our patch. So let's add two
things to our spec file:

+   - A \texttt{%patch} tag line pointing to our patch file
+   - A \texttt{%patch} macro in our \texttt{%prep} script

Easy enough. At the top of the spec file, along with the other tags, let's add

```
Patch: amanda-2.3.0-1inux.patch
```

Then we'll make our \texttt{%prep} script look like this:

```
%prep
%setup
%patch -p 1
```

There, that should do it. Let's give that \texttt{-bp} option another try:

```
# rpm -bp amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
+ umask 022
+ echo Executing: %prep
Executing: %prep
+ cd /usr/src/redhat/BUILD
+ cd /usr/src/redhat/BUILD
+ rm -rf amanda-2.3.0
+ gzip -dc /usr/src/redhat/SOURCES/amanda-2.3.0.tar.gz
+ tar -xvzf -
drwxr-xr-x 3/20 0 May 19 22:10 1996 amanda-2.3.0/
-rw-r--r-- 3/20 1389 May 19 22:11 1996 amanda-2.3.0/COPYRIGHT
-rw-r--r-- 3/20 1958 May 19 22:11 1996 amanda-2.3.0/Makefile
-rw-r--r-- 3/20 11036 May 19 22:11 1996 amanda-2.3.0/README
```