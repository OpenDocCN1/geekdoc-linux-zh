# SWAT and smb.conf

SWAT is a network-based Samba configuration tool that uses a Web page interface to enable you to configure your smb.conf file. SWAT is, by far, the easiest and simplest way to configure your Samba server. SWAT provides a simple-to-use Web page interface with buttons, menus, and text boxes for entering values. A simple button bar across the top enables you to select the sections you want to configure. A button bar is even there to add passwords. To see the contents of the smb.conf file as SWAT changes it, click View. The initial screen (HOME) displays the index for Samba documentation (see Figure 37-2). One of SWAT's more helpful features is its context-sensitive help. For each parameter and option SWAT displays, you can click a Help button to display a detailed explanation of the option and examples of its use.

![](bbox=[0.12, 0.43, 0.55, 0.74])

Figure 37-2: SWAT home page

# Activating SWAT

SWAT is normally installed with Samba. SWAT is an xinetd service. As an xinetd service, it will be listed in the /etc/services and /etc/xinetd.d/swat files. The SWAT program uses port 901, as designated in the /etc/services file and shown here:

```
```
swat 901/tcp # Samba Web Administration Tool
```
```

As an xinetd service, SWAT will have its own xinetd file in the /etc/xinetd.d directory, /etc/xinetd.d/swat. SWAT is turned off by default, and its disable option is set to yes. To use SWAT, you will have to change the disable option to no as shown here:

```
```
# default: off
# description: SWAT is the Samba Web Admin Tool. Use swat \
#     to configure your Samba server. To use SWAT, \
# connect to port 901 with your favorite web browser.
service swat
{
    disable = no
    port = 901
    socket_type = stream
```
```