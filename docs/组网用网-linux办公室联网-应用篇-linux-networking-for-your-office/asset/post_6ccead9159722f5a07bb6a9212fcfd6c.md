
## Removing Print Jobs by Using lprm

If you want to stop a print job, either before it begins printing or while it's printing, use the lprm command. For instance, you can type

```
lprm -Plexmark 154
```

to remove the second print job identified by the lpq command just discussed, assuming that the queue name is lexmark. You need to be the owner of that job or root to use lprm on a print job.

### TIP

> If you issue an lprm command on a printing job, printing might stop in the middle of the page. For inkjet and dot-matrix printers, you might need to eject the half-printed page, and possibly reset your printer, to get it to function correctly. You don't need to eject a page from a laser printer, but a reset might be necessary. Many printers have a button or command available on their front panels to accomplish this task.

## Printing a File by Using lpr

The lpr command prints a file from an xterm or text-mode login. For instance, to print a PostScript file called file.ps to a PostScript or Ghostscript-driven printer on the queue lexmark, you would type

```
lpr -Plexmark file.ps
```

Red Hat Linux's standard smart filter can handle a number of formats in addition to PostScript and ASCII text, including GIF images, JPEG images, TeX documents, and Hewlett-Packard's PCL printer language. Other smart filter packages support various combinations of file types. For use with a networked printer, only the PCL, PostScript, and ASCII capabilities are likely to be useful. In fact, the filter's detection algorithms don't always work correctly, so you might find it helpful to create a raw queue for PostScript or PCL printers.

## Managing the Print System by Using lpc

The lpc command is the workhorse printer control command for Linux, but you need to be root to use many of its features. Also, lpc often resides in the /usr/sbin directory, which your shell might not search automatically, so you might need to type the complete pathname to use it (that is, type /usr/sbin/lpc rather than just lpc). I don't give the complete path in the following discussion, however, for brevity's sake.

You use the lpc command to enable or disable queues or to rearrange the order of print jobs.

You'll probably use it mostly for this last function. Suppose that you want to rearrange the order of the jobs in the queue in the previous example so that job 154 prints before job 153. To do so, you would type

```
lpc topq lexmark 154 153
```

The topq parameter tells lpc that you want to place the specified print jobs at the top of the queue in the order that you specify. The lpc command doesn't interrupt printing on the current job, however, so it remains in place (you can kill it with lprm if necessary).

You can also use lpc to entirely disable or enable a queue by using the down or up parameters, as in `lpc down lexmark` or `lpc up lexmark`. Other variants have subtly different effects. You can type `man lpc` at an xterm prompt to read the Linux documentation on lpc. You can type the man command to find more information about the other print queue management commands, too.

## Printer Sharing Security Considerations

As with most networking features, you should be aware of the security implications of running remotely accessible printer queues. The details of these considerations vary substantially from one sharing method to another, but as an overview, you might want to consider the following points:

- An export using UNIX-style lpd sharing uses "trusted host" methods similar to those for network filesystem (NFS) file sharing. You should therefore be careful about what hosts have access to your printer.
- Sharing printers via Samba provides the possibility of fine control on a per-user basis with password requirements.
- Printer sharing via Netatalk involves little security. It uses AppleTalk rather than TCP/IP, though, so it's relatively invulnerable to attack via the Internet.
- As with other network services, there's always the risk that a bug in the server could open your system to a cracker, so you should not make services available unnecessarily. This is especially true if your server is visible to the Internet as a whole.
- Assuming that a server bug doesn't lead to bigger problems, leaving a printer share open without adequate security can allow others to print files. A malicious individual might set a printer to churn out a ream of completely black pages late at night. Because ink and toner are far more expensive than paper, this high-density printout could cost substantially more than the $5 or so the paper costs. Turning off printers at night is therefore a sensible precaution, if your office's work habits allow it.
