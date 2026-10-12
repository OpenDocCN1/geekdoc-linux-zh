real is sorting the packets by the port that the protocol uses. As a result, if we filter just FTP packets using the display filter, we end up getting all packets that used the FTP port. This has the unfortunate effect of not displaying other packets that may contain FTP information.

A useful feature of etherreal is that we can save the captured data in a regular UNIX file and also read capture files created by other software tools, such as tcpdump or snoop. The snoop tool provides the same basic capabilities and features as tcpdump, but is only available for the Sun Solaris platform. In contrast, tcpdump is available for many UNIX systems.

To save data from a capture, just select the Save item from the File menu. When this is done, a dialog box is displayed, as shown in Figure 5.11. If you will be doing a fair amount of capturing, it is recommended that a special directory be created to contain all the files. Also, it may be necessary to label the files with important information about the captured data so that, later on, they can be easily identified. Without complete and appropriate labeling of the files, the only way to know for sure what each capture file contains is to read it into the etherreal software and review it.

When the dialog box first appears, it contains the directory and any associated files from the location where the etherreal program was started. You can specify the destination file explicitly in the Selection: text box, or navigate using the drop-down menu. In this example, the path and filename

```
/home/capture/ftp-traffic-12-10-99.data
```

has been entered in the Selection: text box. As suggested, the filename contains both the type of packets and the date on which the capture took place. In most instances, this should be sufficient; however, additional information such as the name of the system the capture was from, additional protocol information, or other associated information could prove useful in the future. Note also that in the dialog window, three buttons are provided as a convenience to the user. These include Create Dir, Delete File, and Rename File buttons. Clicking the Create Dir button displays a small dialog box that requests the name of a directory to be created. Entering the directory name and clicking the Create button