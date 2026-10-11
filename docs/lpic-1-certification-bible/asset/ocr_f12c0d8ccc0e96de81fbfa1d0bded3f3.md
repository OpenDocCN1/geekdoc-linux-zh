```
IndexOptions FancyIndexing
```

Several other useful `IndexOptions` are available, such as `ScanHTMLTitles`, `IconsAreLinks`, and `FoldersFirst`. `ScanHTMLTitles` reads HTML files and uses the title instead of the filename. `IconsAreLinks` lets users click on the icon and not just the filename. `FoldersFirst` lists folders at the top and files below them.

```
IndexOptions ScanHTMLTitles IconsAreLinks FoldersFirst
```

The following directives let you fine tune the icons used for the listings.

```
DefaultIcon /icons/unknown.gif
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
```

The `AddDescription` directive lets you put a description with a file or set of files that match a pattern.

```
AddDescription "GZIP compressed tar archive" .tgz
```

The `HeaderName` and `ReadmeName` directives specify the display of certain text files. The file defined by `HeaderName` is attached to the top of the directory listing, and `ReadmeName` is appended to the bottom.

```
ReadmeName README
HeaderName HEADER
```

# Authentication

Apache provides authentication mechanisms that allow you to secure directories or entire sites. The most basic form uses a file that holds user accounts and encrypted passwords. Below is a block example that shows the needed directives.

```
<Directory /home/httpd/html/private>
AuthType Basic
AuthName Private
AuthUserFile /etc/web.users
AuthGroupFile /etc/web.groups
Require valid-user
</Directory>
```