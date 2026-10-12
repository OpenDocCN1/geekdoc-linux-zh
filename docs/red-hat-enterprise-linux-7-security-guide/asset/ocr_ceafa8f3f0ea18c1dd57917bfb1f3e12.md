```
Tasks: 2 (limit: 4915)
CGroup: /system.slice/firewalld.service
└─705 /usr/bin/python3 -Es /usr/sbin/firewalld --nofork --nopid
```

Furthermore, it is important to know how `firewalld` is set up and which rules are in force before you try to edit the settings. To display the firewall settings, see Section 5.3.2, “Viewing Current `firewalld` Settings”

# ### 5.3.2. Viewing Current firewalld Settings

# #### 5.3.2.1. Viewing Allowed Services using GUI

To view the list of services using the graphical **firewall-config** tool, press the **Super** key to enter the **Activities Overview**, type `firewall`, and press **Enter**. The `firewall-config` tool appears. You can now view the list of services under the **Services** tab.

Alternatively, to start the graphical firewall configuration tool using the command-line, enter the following command:

```
~]$ firewall-config
```

The **Firewall Configuration** window opens. Note that this command can be run as a normal user, but you are prompted for an administrator password occasionally.