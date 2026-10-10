Each of these menu options is explained here.

+   * Network This menu item opens the configuration dialog boxes and menus that control most of the functions of your workstation on the network.
+   * TCP/IP These menu items can be used to control your workstation's basic networking functionality.

# Network Information Service

Network Information Service (NIS) allows configuration of the NIS domain and options as shown in Figure 10.3. This is a Sun-originated protocol that has found fairly wide acceptance for large UNIX installations. In short, NIS can be used to provide a means for host and user locating and authentication. The specifics and setup can be (and generally are) quite complicated, and the need to configure this would probably apply only if you are trying to integrate your new OpenLinux box into a much larger UNIX population. If that is the case, you can use COAS to configure your box as an NIS client using the following dialog boxes and fields:

![](bbox=[0.08, 0.48, 0.62, 0.62])

+   * Domain Name  NIS domain that your client box is to be part of. Note that this is probably different from your DNS domain name. If you think you need to enable the NIS configuration, make sure that you have all the correct information for these boxes before you start. Badly misconfiguring NIS on your box will cause grief for your Network Administrator and is likely to have unpleasant consequences on your health.
+   * Start NIS Client on Boot  Allows you to start ypsbind on your workstation bootstrap. This allows you to take advantage of NIS services. If the Domain Name box is empty, this toggle box will be grayed out.
+   * NIS Servers  Normally set to broadcast so that it can detect any available NIS servers on the network. Using this dialog box you can manually set up to ten NIS servers that your client workstation will be allowed to bind to. See Figure 10.4.