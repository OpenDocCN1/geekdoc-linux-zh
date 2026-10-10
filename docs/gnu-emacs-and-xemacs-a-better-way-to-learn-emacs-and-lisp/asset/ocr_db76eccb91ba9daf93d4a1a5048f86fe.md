142   Chapter 21: Emacs Games

![](bbox=[0.21, 0.06, 0.82, 0.42])

# Figure 21.1    Dissociated Press

preserves word boundaries and overlaps three words each time a chunk is found and inserted into the new buffer.

# CONX

Jamie Zawinski, early XEmacs developer and former Netscape programmer, ported another word scrambler named Conx to Emacs-Lisp about ten years ago. This one is a lot of fun to play around with. It differs from Dissociated Press in that when you “conx” a buffer or region, the text is analyzed, and a word-frequency tree is generated and maintained in memory. You can then go to other buffers and add them to the tree so that the ultimate output is drawn from all buffers. Some interesting and/or bizarre sentences can be generated when the input buffers are from differing genres and eras of literature.

Conx is included in the XEmacs Misc-games package. It isn’t part of the GNU Emacs distribution, but I have found that it byte-compiles and runs under GNU Emacs. Users of GNU Emacs can unpack the Misc-games package, which can be found on this book’s CD-ROM in the directory /cdrom/packages/xemacs, and copy the conx.el file to their site-lisp directory. Load the file and byte-compile it; the error messages can be ignored. The only part of Conx that doesn’t seem to run correctly is the hybird mode, summoned with the command M-x psychoanalyze-conx.