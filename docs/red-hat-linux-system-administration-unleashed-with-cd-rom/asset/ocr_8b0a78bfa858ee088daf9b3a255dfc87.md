As you can see, there is some duplication between some of the control-panel modules and Linuxconf but this allows you to choose the tool that you prefer. The biggest example of this duplication is the network configuration module. In addition, some of the modules do very little, such as the modem configuration module, which asks you which COM port your modem is on and then creates a symbolic link from that device to /dev/modem. This is not to say that the control-panel is not useful.

For example, configuring PPP using the control-panel is normally quite simple and involves the following steps:

+   1. Configure your modem using the modem configuration tool.
+   2. Select the network configurator from the control-panel shown in Figure 2.2. This will bring up the dialog box shown in Figure 2.3.
+   3. Click on the Interfaces tab, and then click the Add button. This will present a dialog box that you would use to specify an interface type.
+   4. Select type PPP and click the OK button.
+   5. A final dialog box is presented that allows you to specify the phone number to dial, your PPP login name, the associated password, and whether to use PAP authentication. Enter the appropriate values.
+   6. If you want, you can also click the Customize button to set options such as whether to set up a default route, whether the interface should be started at boot time, whether the PPP connection should be restarted if it fails, customize the chat script for logging into your service provider, and so on.
+   7. Once you have saved the configuration information, click the Activate button to test, and you are all set.

![](bbox=[0.18, 0.77, 0.8, 0.9])

In addition to Linuxconf and the control-panel, Red Hat also provides some simple tools to configure specific functionality or devices. Table 2.5 lists a few of these tools and their purpose.