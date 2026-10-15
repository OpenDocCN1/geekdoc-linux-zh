# Removing Print Jobs by Using lprm

If you want to stop a print job, either before it begins printing or while it's printing, use the lprm command. For instance, you can type

```
lprm -Plexmark 153
```

to remove the second print job identified by the lpq command just discussed, assuming that the queue name is lexmark. You need to be the owner of that job or root to use lprm on a print job.

# TIP

> If you issue an lprm command on a printing job, printing might stop in the middle of the page. For inkjet and dot-matrix printers, you might need to eject the half-printed page, and possibly reset your printer, to get it to function correctly. You don't need to eject a page from a laser printer, but a reset might be necessary. Many printers have a button or command available on their front panels to accomplish this task.

# Printing a File by Using lpr

The lpr command prints a file from an xterm or text-mode login. For instance, to print a PostScript file called file.ps to a PostScript or Ghostscript-driven printer on the queue lexmark, you would type

```
lpr -Plexmark file.ps
```

Red Hat Linux's standard smart filter can handle a number of formats in addition to PostScript and ASCII text, including GIF images, JPEG images, TeX documents, and Hewlett-Packard's PCL printer language. Other smart filter packages support various combinations of file types. For use with a networked printer, only the PCL, PostScript, and ASCII capabilities are likely to be useful. In fact, the filter's detection algorithms don't always work correctly, so you might find it helpful to create a raw queue for PostScript or PCL printers.

# Managing the Print System by Using lpc

The lpc command is the workhorse printer control command for Linux, but you need to be root to use many of its features. Also, lpc often resides in the /usr/sbin directory, which your shell might not search automatically, so you might need to type the complete pathname to use it (that is, type /usr/sbin/lpc rather than just lpc). I don't give the complete path in the following discussion, however, for brevity's sake.