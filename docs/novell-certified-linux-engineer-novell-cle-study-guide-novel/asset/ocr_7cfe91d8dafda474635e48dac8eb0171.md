Once you have added the multicast route, you’re ready to start configuring an SLP daemon on your server. As mentioned earlier, you need to choose whether you want to use the slpuaa daemon that comes with NNLS or the OpenSLP daemon. Configuration tasks for both will be covered next.

# Configuring the slpuaa Daemon

If you don’t have OpenSLP installed, the NNLS installation script will auto-matically install the slpuaa daemon on your server. By default, it is con-figured to load an SA and a UA on your server.

Once the slpuaa daemon is installed during the NNLS installation, you can configure it by editing the slpuaa.conf file located in the /etc directory on your server. The default slpuaa.conf file is shown in Figure 5.9.

```
Refer Han pages to set the following parameters and remove # for the parameter
#net.slp.MTU =
#net.slp.isBroadcastOnly =
#net.slp.isMulticastOnly =
#net.slp.MulticastRadius =
#net.slp.useScopes =
#DA.PORT =
```

**FIGURE 5.9**
The slpuaa.conf file.

You can configure the following parameters in the slpuaa.conf file:

+   *   **net.slp.MTU**—This parameter specifies the maximum path unit used by the SA to service requests. The default value is **1400**.

+   *   **net.slp.isBroadcastOnly**—This parameter specifies whether requests are sent as multicasts or as broadcasts. When set to the value of **0** (the default), this parameter configures the daemon to use multicasts only. When set to the value of **1**, it configures the daemon to use broadcasts instead of multicasts.

+   *   **net.slp.isMulticastOnly**—This parameter is used to prevent the local SA from operating in DA mode. When this parameter is set to a value of **1**, the SA will not try to discover DAs on the network when it is started. It will not register its services with DAs it finds. The default value of **0** configures the DA to operate in normal mode.