```
/usr/lib/libartsdsp_st.so
/usr/lib/libartsdsp_st.so.0
/usr/lib/libartsdsp_st.so.0.0.0
/usr/include/kde/arts/kartsdispatcher.h
```

Still nothing useful.

![](bbox=[0.35, 0.38, 0.42, 0.46])

> If your locate command has no output, it might be because you haven't created the initial locate database. Have a look at the man page for details on how to accomplish this simple task.

Let's look in /usr/bin to see what's part of the arts family of applications:

```
# ls /usr/bin/arts*
/usr/bin/artsbuilder   /usr/bin/artsd   /usr/bin/artshell
/usr/bin/artscat      /usr/bin/artsdsp /usr/bin/artswrapper
/usr/bin/arts-config  /usr/bin/artsmessage
/usr/bin/artscontrol  /usr/bin/artsplay
```

Quite a few applications, actually. It's surprising that there's not a single man page for any of it.

3. Let's try one more locate before we give up and jump to a search on Google, or one of the Linux sites on the Web:

```
# locate artscontrol
/usr/bin/artscontrol
/usr/share/apps/artscontrol
/usr/share/apps/artscontrol/artsmidimanagerview.rc
/usr/share/apps/artscontrol/artscontrol.rc
/usr/share/icons/hicolor/16x16/apps/artscontrol.png
/usr/share/applnk/Multimedia/artscontrol.desktop
```

Ah ha! There's a directory called artscontrol in the /usr/share/apps directory. Let's see what else is in that directory that might be relevant to our search:

```
# cd /usr/share/apps
# ls -ld arts*
drwxr-xr-x 4 root root 4096 Jan 11 15:03 artsbuilder
drwxr-xr-x 2 root root 4096 Jan 11 15:03 artscontrol
```

The artscontrol directory looks promising:

```
# ls /usr/share/apps/artscontrol
artscontrol.rc artsmidimanagerview.rc
# more $/artscontrol.rc
more /usr/share/apps/artscontrol/artscontrol.rc
```