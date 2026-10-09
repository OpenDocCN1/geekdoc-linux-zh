```
# make -DBATCH_DELETE_OLD_FILES delete-old
```

I find yes(1) easier, though.

# Obsolete Shared Libraries

Obsolete shared libraries require more care. Many third-party programs link against shared libraries. If you delete the shared library, the program won't run. This can be really, really annoying if you, say, delete the library required by your mission-critical application. The only way to restore service is to recompile the program or replace the shared library. We discuss shared libraries in Chapter 17. If none of your programs require the library, you can delete it. Identifying every program that requires a library is a royal pain, however.

For example, check the list of obsolete shared libraries above. One of the entries is libzfs.so.2. Looking in /lib, I see that we now have libzfs.so.3. Perhaps I shouldn't need two different versions of the ZFS library. This host uses ZFS, though, and I have a whole bunch of ZFS utilities installed. If I remove the old version of libzfs, there's a chance one of those programs won't work anymore. The presence of these obsolete library versions doesn't hurt anything in the short term; you can bring your system back on line with the old libraries in addition to the new ones and reinstall your add-on software in a more leisurely manner. We'll update your ports later in this chapter.

If you believe that none of the libraries listed as old are important and you can safely delete them, back up each before removing it. By just copying the library to an old-libs directory somewhere, you'll make recovery much simpler when you find out that your mission-critical software doesn't work anymore.

You can also copy old libraries into /usr/lib/compat so that your programs will continue to run but the old libraries will be safely out of the way. The problem here is that we both know perfectly well that you're never going to go clean up those libraries.

I prefer to back up the libraries and then remove them from the live system. When I find a program doesn't work, I temporarily copy the missing library from the backup into a compat directory. The added