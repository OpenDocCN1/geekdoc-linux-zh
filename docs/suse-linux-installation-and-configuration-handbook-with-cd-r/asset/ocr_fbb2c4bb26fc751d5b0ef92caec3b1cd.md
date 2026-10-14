request, it needs to put the file to be printed somewhere so it puts it in the directory defined by directory. Note that this directory has to be writeable to all. /tmp is usually a good choice for this directory.

A typical printers section looks like the following:

```
[printers]
comment = All Printers
browseable = no
printable = yes
public = no
guest ok = yes
read only = yes
create mode = 0700
directory = /tmp
```

Your printers should appear in Windows, as shown in Figure 15.4.

FIGURE 15.4
With the modifications you made to Samba, your printers are now shared to the rest of the network.

![](bbox=[0.32, 0.5, 0.82, 0.75])

# Defining Disk Shares

Now that you are familiar with the special shares, it's time to learn more about disk shares. Defining disk shares in Samba is simple. Say you want to define a new disk share called pictures so you can share your image files with the other users on the network. To do this, you would need to enter the following in your smb.conf file:

```
[pictures]
path = /pictures/jpg
comment = My Image files
browseable = yes
read only = yes
guest ok = yes
```