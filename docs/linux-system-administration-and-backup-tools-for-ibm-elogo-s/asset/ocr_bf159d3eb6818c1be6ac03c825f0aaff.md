![](bbox=[0.285, 0.068, 0.818, 0.403])

To export directories to other machines you have to tell the server about the directory you wish to share, who is allowed to access the directory, and under what restrictions. Figure 15 shows how to enter this data.

As with the previous example, you must enter all the relevant data for the share, and press **Add** before proceeding with the configuration. The only difference is that you have two Add buttons.

When exporting NFS share, you are allowed to explicitly specify which hosts are allowed to access the shared directories. Vast2 allows you to keep on adding hosts that are allowed to access the specified share (in the left-hand pane). You of first all are allowed to configure the share before imposing restrictions on who can use it. There is only one option for this, and that is **Directory**. The directory statement simply tells the NFS server what directory you wish to share. Make sure the directory exists; otherwise the server will behave erratically.

Once you have allocated a directory to share, you can start allocating share restrictions.

112 Linux System Administration and Backup for IBM @xSeries and Netfinity