# **OPTIONS**

-ORBInitialHost naserverhost
This options is required. It specifies the host machine on which the na server runs and listens for incoming requests. The **naserverhost** value st specify the port on which the **orb** is running and listening for requests. The value defaults to **localhost** when this option is not specified. If **orbd** and **servertol** are running on different machines, then you st specify the na or IP address of the host on which **orbd** is running.

> *Note:* On OracIe Solaris, you st beco a root user to start a process on a port below 1024. OracIe recommand you use a port nuer above or equal to 1024 for the **naserverport** value.

-Option
Passes **option** to the Java Vintual Machine, where **option** is one of the options described on the reference page for the Java application launcher. For example, **-J-Xms48m** sets the startup mory to 48 MB. See (1).