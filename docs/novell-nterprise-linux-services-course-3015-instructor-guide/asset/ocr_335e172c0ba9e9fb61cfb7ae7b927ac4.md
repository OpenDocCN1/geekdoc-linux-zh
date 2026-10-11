To go directly to the web browser login page, enter

```
https://IP_or_domain/iFolder/Myfiles
```

You can modify this page to fit your company’s internal needs.

+   - **iFolder Management console.** This lets you manage your users' iFolder accounts as well as your iFolder and LDAP servers.

To access the iFolder Management console, open a browser and enter the following:

```
https://IP_or_domain/iFolderServer/Admin
```

where IP_or_domain is the IP address or DNS domain name of your iFolder server.

If you specified different ports during the installation, append the IP address of the server with a colon, followed by the port number. For example:

```
https://192.168.1.1:81/iFolderServer/Admin
```

# Changing the iFolder Data Directory

If, after you have installed iFolder, you need to change the location of the iFolder data directory, do the following:

+   1. Create an ifolderdata folder in the new location. For example, if you want to change the location to /home/ifolderdata, enter the following command:

```
mkdir /home/ifolderdata
```

+   2. Copy the content of /var/opt/novell/ifolderdata to the new location.

+   3. Modify the /etc/opt/novell/ifolder/httpd_ifolder_unix.conf file by changing the iFolderServerRoot parameter to indicate the new directory location.

For example: **iFolderServerRoot “/home/ifolderdata” **