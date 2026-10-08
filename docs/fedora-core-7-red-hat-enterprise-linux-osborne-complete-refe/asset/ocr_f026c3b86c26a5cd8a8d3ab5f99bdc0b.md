**disable** option to no. **chkconfi g** will edit the */etc/xinetd.d/swat* file for you, making this change (see Chapter 21 for more information about **chkconfi g**). The following example shows how you would enable SWAT with the **chkconfi g** command:

```
chkconfi g swat on
```

With **chkconfi g**, you will not have manually restart the xinetd server. However, if you manually edit the file, you will also have to restart the server to have the change take effect. You can do this simply using the **xinetd** script, as shown here:

```
service xinetd restart
```

Before you use SWAT, back up your current **smb.conf** file. SWAT overwrites the original, replacing it with a shorter and more concise version of its own. The **smb.conf** file originally installed lists an extensive number of options with detailed explanations. This is a good learning tool, with excellent examples for creating various kinds of printer and directory sections. Simply make a backup copy:

```
cp /etc/samba/smb.conf /etc/samba/smb.bk
```

# Accessing SWAT

You can start SWAT by opening your browser and enter the IP address 127.0.0.1 with port 901 to access SWAT.

```
http://127.0.0.1:901
```

Instead of 127.0.0.1 you can use **localhost.localdomain**.

```
http://localhost.localdomain:901
```

You can start SWAT from a remote location by entering the address of the Samba server it is running on, along with its port (901), into a Web browser. However, you will first have to enable this feature in the */etc/xinetd.d/swat* file. Currently, the **only_from** line in this file restricts access to just localhost. To enable access from any remote system, just remove this line. If you want to provide access to certain specific hosts, you can list them after 127.0.0.1 on the **only_from** line. Be sure to restart SWAT after any changes. The following example enables access from both 127.0.0.1 and **rabbit.mytrek.com**:

```
only_from 127.0.0.1 rabbit.mytrek.com
```

The following URL entered into a Web browser on a remote system would then display the Web page interface for SWAT on the **turtle.mytrek.com** Samba server:

```
http://turtle.mytrek.com:901
```

You are first asked to enter a username and a password. To configure Samba, you need to enter **root** and the root password. (If you are connecting from a remote system, it is *not* advisable to enter the root password in clear text—see Chapter 29.)