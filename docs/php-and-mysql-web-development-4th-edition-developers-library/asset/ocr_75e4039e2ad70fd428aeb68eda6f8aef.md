When you place options in a group, choose the group that will be used in the context or contexts that you want. The `[server]` group can be used for options that apply to any server, whether standalone or embedded. The `[mysqld]` or `[embedded]` groups can be used for options that apply only to standalone servers or to embedded servers. Similarly, the `[mysqld_safe]` or `[mysql.server]` groups enable you to specify options that apply only to one startup script or the other.

If you launch the server by using the `mysqld_safe` or `mysql.server` script, another way to specify options is to edit the script to pass those options directly to the server. This is a last resort because it has a significant disadvantage: Each time you upgrade MySQL, your modified script gets wiped out with the new version and you must redo your changes.

# 12.2.4  Stopping the Server

To stop the server manually, use `mysqladmin`:  

```
% mysqladmin -p -u root shutdown
```

This works for both Unix and Windows. If you installed the server as a service under Windows, it’s also possible to use the graphical interface offered by the Services Manager to select and stop the server, or to stop the server manually from the command line like this:

```
C:\> net stop MySQL
```

If you have set up the server to start automatically when your system boots, you shouldn’t need to do anything special to stop it automatically at system shutdown time. BSD Unix systems normally shut down processes by sending a `term` signal; they respond to the signal appropriately (or are killed unceremoniously if they fail to do so). `mysqld` responds by terminating when it receives this signal.

For System V-style Unix systems that start the server with `mysql.server`, the shutdown process invokes that script with an argument of `stop` to tell the server to shut down. You can also invoke the script yourself to stop the server manually. For example, if you’ve installed the `mysql.server` script as `/etc/init.d/mysql`, you can invoke it as follows (you’ll need to be root to do this):

```
# /etc/init.d/mysql stop
```

If you run the MySQL server as a Windows service, the service manager automatically tells the server to stop when Windows shuts down. If you do not run the server as a service, you should stop the server manually with `mysqladmin` shutdown or `net stop MySQL` at the command line before shutting down Windows.

# 12.2.5  Regaining Control of the Server When You Cannot Connect to It

Under certain circumstances you might need to restart the server manually if you find that you no longer can connect to it. This presents something of a conundrum, because typically you stop the server by connecting to it so that you can tell it to shut down (for example, by executing a `mysqladmin` shutdown command). How can this situation arise?