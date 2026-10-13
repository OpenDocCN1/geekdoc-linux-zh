Tip: If you have any problems with your virtual machines' controls or with accessing the properties windows for your machines, check the pop-up settings for your browser. It might prevent your browser from showing the configuration windows that you are trying to access.

There are a few specific items that I would like to explain about working with the Management Interface.

# Heartbeat

One of the items that I would like to explain regarding the Management Interface is the meaning of the heartbeat which is displayed next to the power control button of the virtual machines. When the VMware tools have been loaded inside your virtual machine, it will continuously send heartbeats to the GSX Server. When all heartbeats have been received within the minute before the screen was refreshed, the percentage of received heartbeats is 100% and the indicator will be green. When all the heartbeats have not been received, the percentage drops and the indicator will be orange. When you have not loaded the tools, the indicator will be greyed out because in that case the heartbeat is not available at all.

Tip: If you notice strange heartbeat behavior, such as when the percentage is low but the virtual machine is performing very well by itself, check if you have the correct version of the VMware tools loaded inside the guest operating system.

# Start up and shutdown options

The Management Interface also allows you to configure the startup and shutdown options for your virtual machines. It allows you to configure specific actions for your machines when the GSX Server is started on your Windows or Linux host. There might be virtual machines that always need to be available, whereas others should only be started when you need them, such as servers that you use for testing purposes.

By default, the settings are not to start the virtual machine when the host starts and to power off the virtual machine when the host shuts down. You can change these settings from Management Interface. Click on the name (hyperlink) of the virtual machine that you want to manage, or select configure options from the pop-up menu by clicking the arrow next to the virtual machine icon. In the Options tab, you will find the configuration options, as displayed in Figure 35.4.

Note: On a Windows host, the startup option can only be set to automatically start the virtual machine if the machine is configured to run as the local system account or as a specified user.