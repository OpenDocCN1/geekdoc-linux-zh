```
FAX=/usr/bin/fax
EFAX=/usr/bin/efax
EFIX=/usr/bin/efix
DEV=/cua1
CLASS=2
...
```

You get a three-page listing of information about your configuration and your modem's response to the fax script's queries. If you want to see this information at your leisure, redirect the output of the text to a file, for example:

```
# fax test > faxtest.txt
```

You can then read about any error messages or problems with missing software. Assuming everything is okay, you can then try faxing a document using the fax command:

```
# fax send -1 8207442 faxtest.txt
```

The -1 option tells the fax program to send a low-resolution (98 lines per inch) fax, using the fax testing information you created. To send a high-resolution (196 lines per inch) fax, no option is needed, for example:

```
# fax send 8207442 faxtest.txt
faxtest.txt.nn is up-to-date
/usr/bin/efax: Tue Dec 29 21:38:02 1998 efax v 0.8a Copyright 1996
-Ed Casas
efax: 38:02 opened /dev/modem
efax: 38:03 dialing 8207442
efax: 38:26 connected
efax: 38:32 session 196lpi 9600bps 8.5"/215mm 11"/A4 1D - - 0ms
efax: 38:32 header: [98/12/29 21:38 Eric Goldfarb (1 317 123 1234)
--> 8207442 p. 1/3
efax: 39:06 sent 20?2156 lines, 39961+0 bytes, 34 s 9167 bps
efax: 39:09 sent -> faxtest.txt.001
efax: 39:10 header: [98/12/29 21:38 Eric Goldfarb (1 317 123 1234)
--> 8207442 p. 2/3
efax: 39:37 sent 20?2156 lines, 32200+0 bytes, 27 s 9540 bps
efax: 39:40 sent -> faxtest.txt.002
efax: 39:41 header: [98/12/29 21:38 Eric Goldfarb (1 317 123 1234)
--> 8207442 p. 3/3
efax: 39:50 sent 20?2156 lines, 9635+0 bytes, 9 s 8564 bps
efax: 39:55 sent -> faxtest.txt.003
efax: 39:56 done, returning 0
```

As you can see, the fax script automatically recognizes that your file is a text file because of the extension. You can also send PostScript graphics files by fax. If you want to test sending such a graphic, try this command line:

```
# fax send 8207442 /usr/share/ghostscript/4.03/examples/tiger.ps
```