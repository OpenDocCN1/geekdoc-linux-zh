mets as desktop, djet500, lserjet, ljet3, ljet4, necp6, bj10e and bj200
ibmpro. PostScript files which contain only one page (one image)can also
be converted into various graphics formats, such as tiff3 or png256. A con-
version into ASCII text is not possible.

```
-sOutputFile=file.name
```

writes the result of the conversion to the specified file.

```
-sPAPERSIZE=size
```

specifies the paper size of the output. In most cases, a4 must be used, since oth-
erwise gs defaults to the American letter size format which is slightly smaller.

gs works interactively and comes up with an input prompt after pro-
cessed last page. In order to make it clear to gs that the conversion is over, you
ust enter Ctrl+D. If you want to avoid this input, you can specify a second file
called quit.ps which is loaded from /usr/lib/ghostscript/ and only contains the
t'quit'.

The following instruction converts test.ps into the HP LaserJet 3 format. The
results is written to test_out.ps gs to be terminated immediately-after-
wards.

```
gs -sDEVICE=ljet3 -soutputfile.ps -\
  > -sPAPERSIZE=64 -dMOPAUSE test.ps
```

gs exists in various versions which are subject to different copyrights; the most
recent version is 'Aladdin Ghostscript n'. Although this version is freely
available on the Internet, a commercial distribution (such as in Linux distributions)
is only possible with a license agreement. Older versions, after a while, get the name
'GNU Ghostscript n'. They are subject to the GPL, that is distribution (almost)
unrestricted. Depending on the agreement with Aladdin Enterprises, Linux distribu-
tions are therefore partly shipped with Aladdin and partly with Ghostscript.
For the end user, GNU Ghostscript has the disadvantage that the latest drivers are not
yet implemented. Up-to-date information on the different Ghostscript versions can
be found on the Internet:

```
http://www.wisc.edu/ghost/
```

> The man text for gs is fairly comprehensive. In addition, the directory
/usr/share/ghostscript/n/n/doc contains further information about the in-
ternals of GhostScript.

Tip

# PostScript tools (psutils)

With ghostview, you can also select individual pages from a file and store them
as separate PostScript files. If you wish to automate this and other similar tasks, the
commands of the psutils package will be very useful. Some commands are self-
contained programs, others bash or Perl scripts.

For reasons of space, this section cannot contain a detailed description of the
large of commands – but just looking at the listing should give you a good
idea. More details can always be found in the corresponding man pages.