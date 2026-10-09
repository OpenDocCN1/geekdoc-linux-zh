# # The /etc/sysconfig Directory

The /etc/sysconfig directory contains configuration files for services that should be started at system startup. These files contain the settings that describe how these services must be initialized when the system boots. Some of the services listed in the /etc/sysconfig directory include bluetooth, cups, irda, and kdump.

![](bbox=[0.02, 0.21, 0.73, 0.5])

# # The system-config-services Command

The system-config-services command enables you to start and stop system services in the current runlevel. It is an X-based graphical utility and should be run on the GUI terminal. The command opens the **Service Configuration** window, which displays two main tabs; the **Background Services** tab, which is used to control background services and daemons; and the **On Demand Services** tab, which is used to control the services managed by the xinetd command.