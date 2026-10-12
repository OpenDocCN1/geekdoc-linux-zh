Adding exported directories from the main window is very straightforward. Either adding a new share or clicking on Properties for an existing share brings up a dialog box allowing you to adjust the options for that share.

![](bbox=[0.33, 0.18, 0.66, 0.38])

The Basic tab holds settings for the hosts to which you want to export and settings for whether those hosts have write permissions. One of the oversights of the GUI tool is having to select either **ro** or **rw** for the entire list of hosts in the dialog box. If you want to mix **ro** and **rw** hosts, you have to make separate shares in the GUI tool.

Selecting the General Options tab brings up some additional selections that should seem familiar. The Allow Connections from Ports 1024 And Higher option corresponds to the insecure option mentioned earlier. You will probably recognize, without any difficulty, how to specify **insecure\_locks**, **no\_subtree\_check**, and **sync** from the options presented on this tab. The last option, Force sync of write operations immediately, corresponds to the **no\_wdelay** options.

Finally, the User Access tab lets you adjust the squash options. The Treat Remote Root User As Local Root affects the **no\_root\_squash** setting, and Treat All Client Users As Anonymous Users is the **all\_squash** setting. Notice that you can't change the **anongid** or **anongid** options with only **root\_squash** enabled; instead, **all\_squash** has to be enabled.

As usual, the GUI tool provides no support for commenting your /etc/exports file and doesn't mix well with hand edits. In some cases, even a simple, valid, hand-edited /etc/exports file will prove to be unparseable by the GUI tool. As of this writing, the stability of this tool is not quite what it should be, and although we expect that to improve with future updates, you may want to make sure that you understand the format of the exports file in case you find yourself having to edit it by hand.

# # Telling the NFS Server Process About /etc/exports

Once you have an /etc/exports file written up, use the **exportfs** command to tell the NFS server processes to reread the configuration information. The parameters for **exportfs** are found in Table 16-2.