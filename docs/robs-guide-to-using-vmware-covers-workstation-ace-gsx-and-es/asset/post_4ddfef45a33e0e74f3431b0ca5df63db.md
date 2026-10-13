
5. The installation script will prompt you for the directories where the software and documentation will be installed. Here is a list of the default directories that are suggested during installation:

|  |  |
|---|---|
| binary files | /usr/bin |
| init directories (rc0.d/ to rc6.d/) | /etc/init.d |
| init scripts | /etc/init.d |
| VMware Management Interface files | /usr/lib/vmware-mui |
| documentation files | /usr/lib/vmware-mui/doc |

6. When the installation is complete, you will be prompted to run the configuration script. You can accept the default answer (yes) or run the script later by executing the following command:

```
/usr/bin/vmware-config-mui.pl
```

7. The final question is to specify the number of minutes before an http session will time out. The default value is 60 minutes. You can set it to 0 to disable access to the Management Interface or to -1 to configure sessions to never time out.

Now that the installation is complete, you can move to the next chapter where you can read about how the VMware GSX Server can be managed.

## 35 Managing GSX Server and Virtual Machines

The main advantage of VMware GSX Server compared to the Workstation product is that you can manage your server and the virtual machines from remote connections. You do not have to be present at the GSX Server console and there is no need to connect to the host with a remote control utility such as VNC. With VMware GSX Server, management can be performed with Windows and Linux client applications and the Management Interface.

### 35.1 Using the Management Interface

With VMware GSX Server’s Management Interface, you can manage the host itself as well as the virtual machine environment. The web based console allows you to create and delete virtual machines, change the properties of existing machines, and power the machines on and off. The console also allows you to check the status and performance statistics of your GSX Server.

Tip: If you have more than one GSX Server, you need to login to each individual Management Interface to manage them. To simplify the management task and to gain even more control over your virtual machine environment, I recommend that you use the VMware VirtualCenter application. It allows you to manage all your GSX and ESX Servers from one console. You can read more about this application in chapter 1: “Introduction to VMware ESX Server”.

At this point, I am assuming that you have the Management Interface up and running on your server. Instructions on how to install this feature can be found in the previous sections regarding the VMware GSX Server installation.

To login to the Management Interface, start your browser and enter the following URL:

```
https://hostname-or-ip-address:8333
```

An example of the URL and login page is shown in figure 35.1.

![](img/25fe75b93b97a021effaba85db112a52_286_0.png)

Figure 35.1: The login page for the VMware Management Interface.

By default, the Management Interface is configured to use SSL. This is why you need to connect to the server with the HTTPS protocol. If SSL is not available on your server, you can access the service on port number 8222 with the regular HTTP protocol. This is not secure, of course. Your username and password will be transported across the network in clear text. Therefore, if you contact the service through HTTP on port 8222, and if SSL is available, you will automatically be redirected to HTTPS port 8333.

The login page allows you to download the console applications for both Windows and Linux. You can also download these when you are already logged in to the Management Interface.

You can now log in to the Management Interface with a user name and password. This could be Administrator for Windows or root for Linux; however, I suggest that you always use another user name than the default administrative account. This is common practice anyway. The user account that you use to login to the Management Interface will define what rights you have. How to set up the users' rights is explained later on in this chapter.

Using different levels of access for users enables you to create roles in your organization for different types of administrators. For example, you can have a group of administrators that is only allowed to manage the existing Windows servers in your environment and is not allowed to create any new machines. In that case, you can give them the rights that they need on the Windows server virtual machines and the minimal right to see the other servers that are running.

Once you are logged in, you will see a list of virtual machines, their status, and the status information of your VMware GSX Server. An example of a Management Interface browser window is displayed in Figure 35.2.

![](img/25fe75b93b97a021effaba85db112a52_287_0.png)

Figure 35.2: VMware GSX Server and its virtual machines can be managed from the web based Management Interface.

Most features available in the Management Interface are simple and self explanatory. If you need any information about how to create a new virtual machine, change the properties of a machine and so on, I suggest that you check out the VMware GSX Server documentation.

Figure 35.3 displays the controls of the Management Interface that are available for each virtual machine.

![](img/25fe75b93b97a021effaba85db112a52_287_1.png)

Figure 35.3: Every virtual machine can be managed with these controls.

Tip: If you have any problems with your virtual machines' controls or with accessing the properties windows for your machines, check the pop-up settings for your browser. It might prevent your browser from showing the configuration windows that you are trying to access.

There are a few specific items that I would like to explain about working with the Management Interface.

### Heartbeat

One of the items that I would like to explain regarding the Management Interface is the meaning of the heartbeat which is displayed next to the power control button of the virtual machines. When the VMware tools have been loaded inside your virtual machine, it will continuously send heartbeats to the GSX Server. When all heartbeats have been received within the minute before the screen was refreshed, the percentage of received heartbeats is 100% and the indicator will be green. When all the heartbeats have not been received, the percentage drops and the indicator will be orange. When you have not loaded the tools, the indicator will be greyed out because in that case the heartbeat is not available at all.

Tip: If you notice strange heartbeat behavior, such as when the percentage is low but the virtual machine is performing very well by itself, check if you have the correct version of the VMware tools loaded inside the guest operating system.

### Start up and shutdown options

The Management Interface also allows you to configure the startup and shutdown options for your virtual machines. It allows you to configure specific actions for your machines when the GSX Server is started on your Windows or Linux host. There might be virtual machines that always need to be available, whereas others should only be started when you need them, such as servers that you use for testing purposes.

By default, the settings are not to start the virtual machine when the host starts and to power off the virtual machine when the host shuts down. You can change these settings from Management Interface. Click on the name (hyperlink) of the virtual machine that you want to manage, or select configure options from the pop-up menu by clicking the arrow next to the virtual machine icon. In the Options tab, you will find the configuration options, as displayed in Figure 35.4.

Note: On a Windows host, the startup option can only be set to automatically start the virtual machine if the machine is configured to run as the local system account or as a specified user.

![](img/25fe75b93b97a021effaba85db112a52_289_0.png)

Figure 35.4: Startup and shutdown options can be configured on a per virtual machine basis from the Management Interface.

Note: Selecting the shutdown option, and shutdown guest operating system, requires that the VMware tools are running inside the guest operating system. Be aware that only Windows and Linux guests support the shutdown option through the tools.

Tip: VMware GSX Server does not support suspending virtual machines when your host is being shut down. Using suspend and resume saves a lot of time compared to stopping the guest operating system and restarting it again when the GSX Server is started. The GSX Server scripting facility allows you to suspend your machines from a script. Therefore, if you configure a script that is used for a server shutdown, it can suspend your machines. You can even specify the order in which to shutdown the machines. See the scripting section that starts on page 307 for an example of such a script.

### Virtual Machine Configuration

We have looked at the virtual machine configuration options from within the Management Interface. Based on my personal experience, I can say that it is easier to configure those options, which are available both from the virtual machine console or VirtualCenter, from these respective applications. The reason is that the graphical interface on Windows (for both) and Linux (for the Remote Console) allows you to work much easier with the configuration options. One example is attaching an ISO file to a virtual machine. With Management Interface, you have to type the path and filename for the ISO image, whereas in the graphical utilities you can browse to the file.
