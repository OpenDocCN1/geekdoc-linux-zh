# Introduction and Installation SuSE Linux

After the X session starts (which will use vt7 by default), you can jump to the second console and log in by pressing Ctrl+Alt+F2. You can then start a second session at 16-bpp using the K Desktop Environment:

```
# start kde : -1 bpp 16 vt8
```

After KDE starts, you can jump back and forth between the two window managers using the proper combination of keys. SuSE Linux comes with a variety of window managers, and you can jump directly to an X session using several of the following start keywords, including:

+   - fwwm The Fvwm window manager
- fwwm2 The fwwm2 window manager
- icewm The IceWM window manager
- mwm The Motif-like LessIf mwm window manager
- olwm The OpenLook window manager
- windowmaker The WindowMaker window manager

# The Personal X Resource File

Most default settings for the various X clients are found in individual files under the /usr/X11/lib/X11/app-defaults directory. The following is an example:

```
# ls /usr/X11R/lib/X11/app-defaults
```

| Fig Xsysinfo Xfm |
| .. Fig-color Xfader Xsysinfo-color Xgc |
| Axe GV XFontSel XTail Xmag |
| Axinfo Ghostview Xftp XTalk Xman |
| Beforefore Knews XISDownload XTar Xmessage |
| BibView Mgdiff Xinfo XTecad Xmh |
| BibView-color Mwm Xless XTerm Xmine |
| BibView.ger Pixmap Xless-color XTerm-color Tetris |
| Bitmap Views Xload Xextit Tetris.bw |
| Bitmap-color Xanner Xlock Xtscreen Tetris.c |
| Chooser XBlast Xlogo Xarchie Xtoolplaces |
| Clock-color XCalc Xlogo-color Xbl Colors Xvtidune |
| Ddd XCalc-color Mix Colors Zap |
| Display Xclipboard OSview Xditview xltwayplay |
| Edites Xclock RN XScreenSaver Xditvr-chrtr |
| Edites-color Xconsole XSaver Xedit |
| EmiClock Xdb XSm Xfd |