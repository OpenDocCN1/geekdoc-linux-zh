If the browser does not display the directory listing, it will display one of two errors: **Connection refused** or an error page. If you get a **Connection refused** error, make sure that port 80 is not blocked by a firewall (page 901) and check that the server is running:

```
$ ps -ef | grep apache2
max    3479  12869  0 16:55 pts/1    00:00:00 grep apache2
root     5031     1  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
www-data  5032  5031  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
www-data  5088  5031  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
www-data  5092  5031  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
```

If the server is running, confirm that you did not specify a port other than 80 in a **Listen directive**. If you did, the **URL** you specify in the browser must reflect this port number (**http://localhost:port** specifies port **port**). Otherwise, check the error log (*/var/log/httpd/error_log*) for information about what is not working.

To verify that the browser is not at fault, use **telnet** to try to connect to port 80 of the server:

```
$ telnet www.example.com 80
Trying 192.0.34.166...
Connected to www.example.com.
Escape character is '^A'.
CONTROL-^ 
telnet> quit
Connection closed.
```

If **telnet** displays **Connection refused**, it means that the local system cannot connect to the server.

# Modules

Apache is a skeletal program that relies on external modules, called dynamic shared objects (**DSOs**), to provide most of its functionality. In addition to the modules included with Ubuntu Linux, many other modules are available. See *httpd.apache.org/modules* for more information. See *a2enmod* on page 905 for information on enabling modules.

# Configuring modules

> *tip* You can configure some modules by editing their corresponding *.conf* files in the **mods-available** directory.

The names of the files that hold modules start with the prefix **libapache2-mod-** . The following command displays a complete list of modules. You can pipe the list through **grep** to find the module you want. See page 530 for information on *apt-cache*.