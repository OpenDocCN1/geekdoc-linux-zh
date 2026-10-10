Besides using permanent as the service for Redirect (which results in a redirect status 301), you could instead use temp (a redirect status of 302), seeother (a replaced status of 303), or gone (a permanently removed status of 401). You could also give any status code between 300 and 399 as the service, which represent different error responses. (These numbers are HTTP status codes.)

> **CROSS REFERENCE:** The HTTP status codes are defined as part of the HTTP protocol in RFC 2616. Refer to that document at www.w3.org/Protocols/rfc2616/rfc2616.txt.

# ## Defining indexing

It’s possible to have your Apache server show different icons for different types of files. To use this feature, `IndexOptions` should be set to `FancyIndexing`, and `AddIconByEncoding`, `AddIconByType`, and `AddIcon` directives should be used:

```
# Directives controlling display of server-generated directory listings.

# FancyIndexing is if you want fancy directory indexing or standard.
# VersionSort is whether files containing version numbers should be
# compared in the natural way, so that 'apache-1.3.9.tar' is placed
# before 'apache-1.3.12.tar'.
#
IndexOptions FancyIndexing VersionSort NameWidth=* HTMOTable
#
# AddIcon* directives tell the server which icon to show for different
# files or filename extensions. These are only displayed for
# FancyIndexed directories.
#
AddIconByEncoding (CMP, /icons/compressed.gif) x-compress x-gzip

AddIconByType (TXT, /icons/text.gif) text/*
AddIconByType (IMG, /icons/image2.gif) image/*
AddIconByType (SND, /icons/sound2.gif) audio/*
AddIconByType (VID, /icons/movie.gif) video/*

AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gz .vrml .vrm .iv
AddIcon /icons/compressed.gif .Z .z .tgz .gz .zip
AddIcon /icons/a.gif .ai .eps
AddIcon /icons/layout.gif .html .shtml .htm .pdf
AddIcon /icons/txt.gif .txt
AddIcon /icons/c.gif .c
AddIcon /icons/p.gif .pl .py
AddIcon /icons/f.gif .for
AddIcon /icons/dvi.gif .dvi
AddIcon /icons/unencoded.gif .uu
```