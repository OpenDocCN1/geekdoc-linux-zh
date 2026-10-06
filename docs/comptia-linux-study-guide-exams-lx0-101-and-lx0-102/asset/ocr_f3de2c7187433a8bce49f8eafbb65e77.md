# Chapter 2 - Managing Software

Thus, to change ld.so.conf in Gentoo or other distributions that use this mechanism, you should add or edit files in /etc/env.d and then type env-update to do the job.

Generally speaking, there's seldom a need to change the library path systemwide. Library packages usually install themselves in directories that are already on the path or add their paths automatically. The main reason to make such changes would be if you installed a library package, or a program that creates its own libraries, in an unusual location via a mechanism other than your distribution's package utility. For instance, you might compile a library from source code and then update your library path in this way.

After you change your library path, you use ldconfig to have your programs use the new path, as described later in "Library Management Commands."

> In addition to the directories specified in /etc/ld.so.conf, Linux refers to the trusted library directories, /lib and /usr/lib. These directories are always on the library path, even if they aren't listed in ld.so.conf.

# Temporarily Changing the Path

Sometimes, changing the path permanently and globally is unnecessary and inappropriate. For instance, you might want to test the effect of a new library before using it for all your programs. To do so, you could install the shared libraries in an unusual location and then set the LD_LIBRARY_PATH environment variable. This environment variable specifies additional directories the system is to search for libraries.

> Chapter 9, "Writing Scripts, Configuring Email, and Using Databases," describes environment variables in more detail.

To set the LD_LIBRARY_PATH environment variable using the bash shell, you can type a command like this:

```
$ LD_LIBRARY_PATH=/usr/local/testlib:/opt/newlib
```

This line defines two directories, /usr/local/testlib and /opt/newlib, or as many as you like, separated by colons: Directories are added to the start of the search path, which means they take precedence over other directories. This fact is handy when you're testing replacement libraries, but it can cause problems if users manage to set this environment variable inappropriately.

You can set this environment variable permanently in a user's shell startup script, as described in Chapter 9. Doing so means the user always use the specified library paths