# # NIS Clients

For a host to use NIS on your network, you first need to specify your NIS domain name on that host. In addition, your NIS clients need to know the name of your NIS server. If you installed Linux on a network already running NIS, you may have already entered this information during the installation process.

# ## Specifying the NIS Domain and Server

You can specify your NIS domain name and server with the authconfig-gtk tool, which you can access from the System Settings window. In that window, select Authentication. This opens the Authentication Configuration window. On the User Information panel, click the Configure NIS button to open a dialog where you can enter the name of the NIS domain as well as the NIS server. Be sure to also enable NIS on the User Information panel. The NIS domain will be saved in the /etc/sysconfig/network file, and the NIS server, in the /etc/yp.conf file.

# ## Accessing the Server

Each NIS client host on your network then has to run the ypbind NIS client to access the server. In the client’s /etc/yp.conf file, you need to specify the NIS server it will use. The following entry would reference the NIS server at 192.168.1.1:

```
ypserver 192.168.1.1
```

Alternatively, you can specify the NIS domain name and the server it uses:

```
domain mydomain.nis  server servername
```

The authconfig-gtk tool will make the following entry in /etc/yp.conf for the myturtle.nis NIS domain using the turtle.mytrek.com server:

```
domain myturtles.nis  server turtle.mytrek.com
```

To start the NIS client, you run the ypbind script:

```
service  ypbind  start
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