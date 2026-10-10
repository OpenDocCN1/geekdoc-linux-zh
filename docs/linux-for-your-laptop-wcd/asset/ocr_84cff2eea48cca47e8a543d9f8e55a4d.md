You can then write the new image to create a new CD-ROM. There are special tricks and steps you need to take to write audio CDs, to mix and match audio tracks to create custom CDs of .mp3 files, or to back up your notebooks’ hard drive directly to a backup CD. See the CD-Writing HOWTO under the /usr/doc/HOWTO directory for details (or browse to http://www.linuxdoc.org).

# Graphical Interface Clients

Again, just as you can use the command line to copy, create, and write CDR and CD-RW disks, life gets much easier when you use a graphical interface client to do all the hard work. One of the best programs to use with Linux to create CDRs and CDRW drives is X-CD-Roast. You’ll find this X11 software package (a front end to the utilities discussed previously) included with nearly all modern Linux distributions.

Start the client from the command line like this:

```
# xcdroast &
```

When you start the program for the first time, you’ll be asked to enter xcdroast’s setup dialog box shown in Figure 18.16.

Click on xcdroast’s Setup tab to designate your CD-Writer and CD-Reader devices. This client is even more efficient when you use it on a notebook with two CD-ROMs (internal and external). You’ll also need to designate temporary hard drive space and an image mount point. If you want to verify audio tracks, you need to make sure Linux is configured to work with your notebook’s sound system.

![](bbox=[0.07, 0.64, 0.58, 0.97])