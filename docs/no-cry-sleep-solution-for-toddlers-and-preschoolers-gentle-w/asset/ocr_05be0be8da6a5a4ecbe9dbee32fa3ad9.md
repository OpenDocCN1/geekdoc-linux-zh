# Accessing the Server

Each NIS client host on your network then has to run the ypbind NIS client to access the server. In the client’s /etc/yp.conf file, you need to specify the NIS server it will use. The following entry would reference the NIS server at 192.168.1.1:

```
ypserver 192.168.1.1
```

Alternatively, you can specify the NIS domain name and the server it uses:

```
domain mydomain.nis server servername
```

The authconfig-gtk tool will make the following entry in /etc/yp.conf for the myturtle.nis NIS domain using the turtle.mytrek.com server:

```
domain myturtles.nis server turtle.mytrek.com
```

To start the NIS client, you run the ypbind script:

```
service ypbind start
```

Then, to check that all is working, you can use ypcat to try to list the NIS password file:

```
ypcat passwd.
```

You can use ypcat to list any of the NIS configuration files. The ypwhich command will display the name of the NIS server your client is using. ypmatch can be used to find a particular entry in a configuration file.

```
ypmatch cecelia passwd.
```

Users can change their passwords in the NIS passwd file by using the yppasswd command. It works the same as the passwd command. You will also have to have the yppasswd daemon running.

# Specifying Configuration Files with nsswitch.conf

To ensure that the client accesses the NIS server for a particular configuration file, you should specify nisplus in file’s entry in the /etc/nsswitch.conf file. The nisplus option refers to the NIS version 3 used currently on Red Hat. The nis option is used to refer to the older NIS version 2. The /etc/nsswitch.conf file specifies where a host should look for certain kinds of information. For example, the following entry says to check the local configuration files (files) first and then the NIS server (nisplus) for passwords data:

```
passwd: files nisplus
```

The files designation says to first use the system’s own files, those on the local host. nis says to look up entries in the NIS files, accessing the NIS server. nisplus says to use NIS+ files maintained by the NIS+ server. dns says to perform DNS lookups; it can only be used on files like hosts that contain hostnames. These are some standard entries: