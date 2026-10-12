comp.laser-printers newsgroup by Dale Carstensen, for increasing the serial port speed of the Apple LaserWriter Plus to 19200:

```
```
#!/
0000 % Server Password
statussedic begin 25 scbatch 0 ne exch 19200 ne or
{ serverdict begin exitserver} {pop end stop} ifelse
statussedic begin
25 19200 0 setscbatch
end % note
```
```

line has an actual CTRL-D

See Appendix D in the *RedBook*, Adobe's PostScript language reference manual, for more information about LaserWriters, or peruse comp.laser-printers for hints on setting up your laser printer. Also read the file `Pstiles.htm` under the `/usr/share/ghostscript/5.50` directory for information about the numerous PostScript printer utilities included in the Ghostscript distribution.

Most desktop users, however, have a printer attached to the parallel printer port, so I'll first concentrate on `/dev/lp`.

# # What Printer Should I Use with Linux?

Nearly any printer that uses your computer's serial or parallel port should work. One might think that a PostScript printer is the best printer to use with Linux because many programs and text utilities used with Linux and ported from other UNIX systems output graphics and text as PostScript. However, another great reason to use Linux, and Red Hat's distribution of Linux, is that through the magic of software, your S99 inkjet printer can also print PostScript documents—even in color. That's a bargain!

# **New PPA Printer Support!**

Even printers using Printing Performance Architecture (PPA), such as the HP 720, 820, or 1000-series printers, which in the past required a special software driver available only for Windows, are now supported! Thanks to early efforts by Tim Norman, even HP 710C, 712C, 720C, 722C, 820Cs, 820Cs, 1000CSe, and 1000Cxi printer users can now enjoy printing. Red Hat Linux now incorporates supporting filters that provide various color modes. See this chapter's section “`printtool`—The Red Hat Linux Print System Manager” for details on installing support.

![](bbox=[0.88, 0.6, 0.95, 0.8])