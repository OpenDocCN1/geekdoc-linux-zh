# Feature

# Networks

# MONITOR AND MANAGE YOUR SERVER USING AJENTI

Ajenti provides one central location to configure and monitor your server and allows a consistent way to manage Linux systems across its supported distros, and boasts an easy-to-use dashboard that is customised.

Choose your base, then follow the provided instructions to install the software. After installing it, start Ajenti with the following command:

```
# sudo service ajenti start
```

Ajenti is available at http://localhost:8081, the default username is admin. You can change this password as you wish - head to Password from the left bar and change your password to something stronger. Installing Ajenti generates a self-signed certificate which is okay for normal usage.

You can change the certificate by providing a pem file at Configure > General > SSL > Path to certificate. If you are using a proxy at 8000 you may not need to

to start Ajenti. To change the port for Ajenti, edit /ajenti/config.json and change the port in the bind section: 

```
{
  "bind": {
    "host": "0.0.0.0",
    "port": 8081
  }
}
```

To monitor your server, select Dashboard from the menu bar to see widgets data related to the system. To refresh click the list icon at the top of the dashboard. To configure the various systems, processes and users, you can go to the System section of the menu bar. For example the Apache server, MySQL and Samba, go to the Services section of the menu bar. You can also manage the server by clicking Services > Services section.

# MONITORING TOOLS

Dashboard is an interactive viewer that shows all your system in an accessible interface. You can open disk and list processes and take action on processes like killing them. The file list shows files which is very handy when you need to mount a disk and want to know which process is using.

# AJENTI AT A GLANCE

![](bbox=[0.225, 0.583, 0.735, 0.863])

# SPECIFIC CONFIGURATION

Where you have to configure the features of Ajenti. Use this to configure ports, SSL and sign-allows to view the status of installed plugins.

# SYSTEM CONFIGURATION

All of the system-related configuration takes place here, including hosts and filesystems. You can use this to install and update packages.

# SERVICES CONFIGURATION

Here you can find a list of installed services. You can use this to check the status of a service, and start stop

# DASHBOARD

Dashboard is a collection of widgets showing a little information about the system. Additional widgets can be Add New Widgets. You have the option to refresh/autore the widget data.

# COMMON TOOLS

This provides you with easy access to text editor, task manager and help with browser. These tools give you a help when working with the browser you are using.

# SERVER PACKAGES CONFIGURATION

This is where you configure settings for server packages. Depending on what you installed services, this list will have Apache, MySQL, NFS, Netatalk and Samba.

26