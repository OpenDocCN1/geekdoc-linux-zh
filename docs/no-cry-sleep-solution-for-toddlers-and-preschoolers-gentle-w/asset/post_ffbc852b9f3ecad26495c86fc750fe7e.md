
# SWAT and smb.conf

SWAT is a network-based Samba configuration tool that uses a Web page interface to enable you to configure your smb.conf file. SWAT is, by far, the easiest and simplest way to configure your Samba server. SWAT provides a simple-to-use Web page interface with buttons, menus, and text boxes for entering values. A simple button bar across the top enables you to select the sections you want to configure. A button bar is even there to add passwords. To see the contents of the smb.conf file as SWAT changes it, click View. The initial screen (HOME) displays the index for Samba documentation (see Figure 37-2). One of SWAT’s more helpful features is its context-sensitive help. For each parameter and option SWAT displays, you can click a Help button to display a detailed explanation of the option and examples of its use.

![](img/6c226e8ba1efd427dec3bf582418d33f_767_0.png)

## Activating SWAT

SWAT is normally installed with Samba. SWAT is an xinetd service. As an xinetd service, it will be listed in the /etc/services and /etc/xinetd.d/swat files. The SWAT program uses port 901, as designated in the /etc/services file and shown here:

```
swat 901/tcp # Samba Web Administration Tool
```

As an xinetd service, SWAT will have its own xinetd file in the /etc/xinetd.d directory, /etc/xinetd.d/swat. SWAT is turned off by default, and its disable option is set to yes. To use SWAT, you will have to change the disable option to no as shown here:

```
# default: off
# description: SWAT is the Samba Web Admin Tool. Use swat \
#           to configure your Samba server. To use SWAT, \
#           connect to port 901 with your favorite web browser.
service swat
{
    disable = no
    port = 901
    socket_type = stream
    wait = no
    only_from = 127.0.0.1
    user = root
    server = /usr/sbin/swat
    log_on_failure += USERID
}
```

You can do this by using either chkconfig or the Service Configuration tool to turn on the SWAT service or by manually editing the /etc/xinetd.d/swat file and changing the disable option to no. chkconfig will edit the /etc/xinetd.d/swat file for you, making this change (see Chapter 20 for more information about chkconfig). The following example shows how you would enable SWAT with the chkconfig command:

```
chkconfig swat on
```

With chkconfig, you will not have to manually restart the xinetd server. However, if you manually edit the file, you will also have to restart the server to have the change take effect. On Red Hat, you can do this simply using the xinetd script, as shown here:

```
service xinetd restart
```

Before you use SWAT, back up your current smb.conf file. SWAT overwrites the original, replacing it with a shorter and more concise version of its own. The smb.conf file, when originally installed, lists an extensive number of options with detailed explanations. This is a good learning tool, with excellent examples for creating various kinds of printer and directory sections. Simply make a backup copy:

```
cp /etc/samba/smb.conf /etc/samba/smb.bk
```

## Accessing SWAT

You can start SWAT by selecting the Samba Configuration entry in the GNOME or KDE System menu. This will open your Web browser to the SWAT page using the localhost IP address, 127.0.0.1 and port 901, as shown in Figure 37-2. You can also open your browser and enter the IP address 127.0.0.1 with port 901 to access SWAT.

```
http://127.0.0.1:901
```

You can start SWAT from a remote location by entering the address of the Samba server it is running on, along with its port (901) into a Web browser. However, you will first have to enable this feature in the /etc/xinetd.d/swat file. Currently, the only_from line in this file restricts access to just localhost. To enable access from any remote system, just remove this line. If you want to provide access to certain specific hosts, you can list them after 127.0.0.1 on the only_from line. Be sure to restart SWAT after any changes. The following example enables access from both 127.0.0.1 and rabbit.mytrek.com:

```
only_from 127.0.0.1 rabbit.mytrek.com
```

The following URL entered into a Web browser on a remote system would then display the Web page interface for SWAT on the turtle.mytrek.com Samba server:

```
http://turtle.mytrek.com:901
```

You are first asked to enter a username and a password. To configure Samba, you need to enter root and the root password. (If you are connecting from a remote system, it is not advisable to enter the root password in clear text—see Chapter 28.)

## SWAT Configuration Pages

The main SWAT page is displayed with a button bar, with buttons for links for HOME, GLOBAL, SHARES, PRINTERS, STATUS, VIEW, and PASSWORD (see Table 37-2). You can use STATUS to list your active SMB network connections.

| Page | Description |
|------|-------------|
| HOME | SWAT home page listing documentation resources. |
| GLOBALS | Configures the global section for Samba. |
| SHARES | Selects and configures directories to be shared (shares). |
| PRINTERS | Sets up access to printers. |
| STATUS | Checks the status of the Samba server, both smbd and nmbd; lists clients currently active and the actions they are performing. You can restart, stop, or start the Samba server from this page. |
| VIEW | Displays the smb.conf configuration file. |
| PASSWORD | Sets up password access for the server and users that have access. |
