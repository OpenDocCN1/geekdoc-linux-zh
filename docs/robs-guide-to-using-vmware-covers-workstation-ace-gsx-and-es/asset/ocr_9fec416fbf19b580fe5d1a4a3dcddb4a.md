Also modify your services file (/etc/services). Find the vmware-authd entry and change the port number that you want to use.

```
vmware-authd 902/tcp
```

Next, you need to restart the xinetd daemon:

```
/etc/init.d/xinetd restart
```

# 37.3 Setting the Session Length for the VMware Management Interface and Disabling Login

The default timeout setting for sessions with the Management interface is 60 minutes. This timeout value can be changed by modifying the Management Interface configuration file.

# Windows

Change the setting of vmware_SESSION_LENGTH in the file C:\Program Files\VMware\VMware Management Interface\htdocs\init.pl

```
$ENV{vmware_SESSION_LENGTH} = 60;
```

# Linux

For Linux, you need to run the configuration script for the Management Utility. This will prompt you for the number of minutes that you want.

```
/usr/bin/vmware-config-mui.pl
```

For both Windows and Linux, you can also disable the access to the Management Interface by specifying 0 as the timeout value. The login screen will display a message to warn users that login is prohibited: The VMware Management Interface is closed and no logins are permitted.

When you specify -1 in the configuration file, the sessions will never time out.

# 37.4 Accessing VMware GSX Server Log Files

If you experience any problems with your VMware GSX Server environment, the log files are a good place to start your investigation. This paragraph simply points you to the correct log file locations.

# Virtual machine log file

Every virtual machine keeps its own log of what's happening. It is created in the virtual machine's configuration directory, which is where the .vmx file is located.