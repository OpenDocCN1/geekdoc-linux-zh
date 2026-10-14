⇒ To convert the PostScript file resume.ps to fax format, type (all on one line):

```
$ gs -q -sDEVICE=tiffg3 -dSAFER -dNOPAUSE
-sOutputFile=resume.fax resume.ps < /dev/null [RET]
```

This command writes a copy of the file resume.ps to the file resume.fax in TIFFG3 format, which you can then send as a fax. The original PostScript file is not altered.

NOTES: For more on using gs, see Recipe 25.3.1 [Preparing a PostScript File for Printing], page 518.

# METHOD #4

teTeX
DEB: tetex-base
    tetex-bin
    tetex-doc
    tetex-extra
RPM: tetex
WWW: http://www.tug.org/teTeX/

Use dvi2fax to convert a DVI file made from TeX into 'tiffg3' format for faxing.

It takes as options either '-hi' for high resolution, outputting at 204x196 dpi (the default), or '-lo' for low resolution, outputting at 204x98 dpi.

Give as an argument the name of the DVI file to convert; giving the '.dvi' extension is optional.

⇒ To convert the file 'proposal.let.dvi' to low resolution fax-format files, type:

```
$ dvi2fax -lo proposal.let [RET]
```

Each page of input is written to its own file, numbered in order and with a '.fax' extension.

# 31.3 Calling Out on a Modem

Minicom
DEB: minicom
RPM: minicom