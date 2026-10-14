# Conversion to PCL5e or PCL6

A PostScript file is converted to the printer-specific format for a PCL5e or PCL6 printer with the command

```
```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \\
    -sDEVICE=ljet3 -r300x300 \
    /usr/share/doc/packages/ghostscript/colorcir.ps quit.ps
```
```

where the command is given in a single line without backslash ('\\'). The assumption is also made that the file /tmp/out.prn does not exist yet.

# Conversion to PCL3

A PostScript file is converted to the printer-specific format for a PCL3 printer with the following commands:

```
```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \\
    -sDEVICE=hpdj -r300x300 \
    -sModel=500 -sColorMode=mono -dCompressionMethod=0 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \\
    quit.ps
```
```

```
```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \\
    -sDEVICE=cdj300 -r300x300 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \\
    quit.ps
```
```

```
```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \\
    -sDEVICE=cdj500 -r300x300 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \\
    quit.ps
```
```

```
```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \\
    -sDEVICE=cdj550 -r300x300 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \\
    quit.ps
```
```

(Enter each command as a single line and disregard the '\\'.)

# Conversion to ESC/P, ESC/P2 or ESC/P Dot-Matrix

A PostScript file is converted to the printer-specific format for ESC/P2, ESC/P or ESC/P dot matrix printers with the commands

```
```text
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \\
    @stcany.upp \\
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \\
    quit.ps
```
```