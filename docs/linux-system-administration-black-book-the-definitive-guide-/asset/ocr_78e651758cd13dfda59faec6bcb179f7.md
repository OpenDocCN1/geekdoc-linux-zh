# 13. The Apache Web Server

The *MIME-encoding* portion represents the method used to wrap encoding or encryption around a file. This method is used so that the file can be transmitted more quickly and yet come out whole and understandable by the machine on the other end. The two encodings listed by default are the only two typically used on the Web today.

The following is the next directive set:

```
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
```

**AddIconByType** is used in exactly the same format that **AddIconByEncoding** is. In this case, however, many more types are available than are listed here. The current list of all available MIME media types is provided by the Internet Assigned Numbers Authority (IANA) at www.isi.edu/in-notes/iana/assignments/media-types/media-types.

When you add by type, you are telling Apache to make a guess about the file type. If you want to state explicitly which icon to use for which file type, use the **AddIcon** directive. The first four **AddIcon** lines are shown here:

```
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gz .vrml .vrm .iv
```

An **AddIcon** directive is used in this format:

```
AddIcon icon ext
```

The *icon* portion of the directive is the path—written in an absolute format but really relative to DocumentRoot—to the icon you are assigning. To tell Apache to use this icon to show particular kinds of files, place a space-separated list of extensions in the *ext* portion.

Even the most experienced Web administrator cannot anticipate every file extension that users or clients may include on their Web sites. The **DefaultIcon** directive allows you to ensure that at least some kind of icon is used for unknowns:

```
DefaultIcon /icons/unknown.gif
```

Next is more icon indexing information: