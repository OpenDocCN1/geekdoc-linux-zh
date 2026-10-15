# Accessing SWAT

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

# SWAT Configuration Pages

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