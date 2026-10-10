# 782  Appendix A

or later contain no timezone information, and a “newer” file from an east ern timezone may, in fact, be older:

```
unzip -fo sources
```

To extract newer versions of the files already in the current directory and to create any files not already there (same caveat as previous example):

```
unzip -uo sources
```

To display a diagnostic screen showing which unzip and *zipinfo* options are stored in environment variables, whether decryption support was compiled in, the compiler with which unzip was compiled, etc.:

```
unzip -v
```

In the last five examples, assume that UNZIP or UNZIP_OPTS is set to -q. To do a singly quiet listing:

```
unzip -l file.zip
```

To do a doubly quiet listing:

```
unzip -ql file.zip
```

(Note that the “-ql.zip” is generally not necessary.) To do a standard listing:

```
unzip -qql file.zip
```

or

```
unzip -l -q file.zip
```

or

```
unzip -l -q -q file.zip
```

Extra minuses don’t hurt.

# TIPS

The current maintainer, being a lazy sort, finds it very useful to define a pair of aliases: *tt* for “unzip -tq” and *ii* for “unzip -Z” (or “zipinfo”). One may then simply type “*tt zipfile*” to test an archive, something that is worth making a habit of doing. With luck unzip will report “**No errors detected in compressed data of zip-file.zip,**” after which one may breathe a sigh of relief.

The maintainer also finds it useful to set the UNZIPINFO environment variable to “-AL” and is tempted to add “-C” as well. His UNZIPINFO variable is set to “-Z”.