+   - external SCSI drives
+   - CD-ROM drives (external and internal)
+   - SCSI/Ether SBUS expansion cards
+   - Any original equipment Sun monitor for the above framebuffer

A partial list of *unsupported* hardware:

+   - VME based sun4m machines, such as the 4/690
+   - sun4d (SS1000, SS2000)
+   - sun4u (UltraSparc1, UltraSparc2, EnterPrise UltraSparc servers)
+   - sun4 architecture
+   - Eurocard sundc machines, called the 'sun4e' under Solaris2.4 and others, are not supported. These are VME-bus sun4c machines, to which the kernel has not been ported yet.

# ### 4.2 Booting from Floppy

# #### 4.2.1 Making a Boot Floppy

If your SPARC system has a floppy drive, you can boot the Red Hat Linux installation program from a floppy diskette. The boot floppy image is located on the **images/** directory on your Red Hat CD.

To create the boot floppy, you can use **rawrite.exe** under MS-DOS (located on your Red Hat Linux/SPARC CD in the **dosutils** directory), or you can use **dd** under Linux or Unix. Under MS-DOS, you would enter the following commands (assuming the CD-ROM is drive d:):

```
d:
 cd \images
 \dosutils\rawrite.exe
```