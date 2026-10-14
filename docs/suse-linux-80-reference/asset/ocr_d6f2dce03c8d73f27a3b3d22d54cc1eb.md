**Paper tray selection** — To activate the default paper tray with 0 or the paper tray with the number 2, for example, create the files `/etc/lpd/filter/test/tray0.ps` and `/etc/lpd/filter/test/tray2.ps` as follows:

```
```postscript
%!PS
statusdict /setpapertray known
statusdict begin 0 setpapertray end if pop
```
```

*File 22: /etc/lpd/filter/test/tray0.ps: Activating Paper Tray 0*

```
```postscript
%!PS
statusdict /setpapertray known
statusdict begin 2 setpapertray end if pop
```
```

*File 23: /etc/lpd/filter/test/tray2.ps: Activating Paper Tray 2*

**Margin settings** — To change the margin settings, create the file `/etc/lpd/filter/test/margin.ps` as follows:

```
```postscript
%!PS
<<
/.HWMargins [left bottom right top]
/PageSize [width height]
/Margins [left-offset top-offset]
>>
setpagedevice
```
```

*File 24: /etc/lpd/filter/test/margin.ps: Margin Settings*

The margin settings left, bottom, right, and top and the paper size width and height must be specified in dots, where one dot is 1/72 inches (approx. 0.35 mm). The margin offsets left-offset and top-offset, on the other hand, should be specified in dot matrices, depending on the resolution.

If only the position of the printout should be shifted on the paper, the following file is sufficient: `/etc/lpd/filter/test/offset.ps`

```
```postscript
%!PS
<< /Margins [left-offset top-offset] >> setpagedevice
```
```

*File 25: /etc/lpd/filter/test/offset.ps: Position of the Printout*