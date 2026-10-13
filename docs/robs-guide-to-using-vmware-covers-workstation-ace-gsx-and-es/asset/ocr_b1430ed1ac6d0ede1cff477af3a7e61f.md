# 35 Managing GSX Server and Virtual Machines

The main advantage of VMware GSX Server compared to the Workstation product is that you can manage your server and the virtual machines from remote connections. You do not have to be present at the GSX Server console and there is no need to connect to the host with a remote control utility such as VNC. With VMware GSX Server, management can be performed with Windows and Linux client applications and the Management Interface.

# 35.1 Using the Management Interface

With VMware GSX Server’s Management Interface, you can manage the host itself as well as the virtual machine environment. The web based console allows you to create and delete virtual machines, change the properties of existing machines, and power the machines on and off. The console also allows you to check the status and performance statistics of your GSX Server.

Tip: If you have more than one GSX Server, you need to login to each individual Management Interface to manage them. To simplify the management task and to gain even more control over your virtual machine environment, I recommend that you use the VMware VirtualCenter application. It allows you to manage all your GSX and ESX Servers from one console. You can read more about this application in chapter 1: “Introduction to VMware ESX Server”.

At this point, I am assuming that you have the Management Interface up and running on your server. Instructions on how to install this feature can be found in the previous sections regarding the VMware GSX Server installation.

To login to the Management Interface, start your browser and enter the following URL:

```
https://hostname-or-ip-address:8333
```

An example of the URL and login page is shown in figure 35.1.