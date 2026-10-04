# Service Configuration

We mentioned previously that systems start a large number of default services by default. An example of this can be seen in Figure 14.8.This is a dangerous configuration to place on any network. Many services started by default, have had in the past, security issues that could allow an attacker to gain unauthorized access. This also extends to processes on the host by default. As we can see in Figure 14.9, a number of default processes are also started that may have security implications.

# Figure 14.8 Default Services Started on an Example Unix System

![](bbox=[0.228, 0.318, 0.709, 0.628])

By this, it is entirely necessary to disable some, if not all services started on the host. The location and starting of services is usually unpredictable by either the init or inetd process. To eliminate potentially risky services started by default, we must edit the init and inetd configurations.

Most runs are controlled by inetd by the inetd configuration file, typically /etc/inetd.conf. Many of the services started via inetd are obscure, and sometimes there is fear about breaking a system by disabling all the running services. A rule of thumb: if you do not know the purpose of a service, do not run it.

Typically, the safest best is to create a backup of the inetd.conf file, named something like inetd.conf.bak. Edit the inetd.conf file to disable all unnecessary services. Unless the system is rebooted after configuring the inetd.conf file, the inetd service either be restarted by the HUP signal, or killed afterwards.