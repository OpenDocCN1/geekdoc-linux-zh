The device name is `ppp0` (which is associated with the configuration file `ifcfg-ppp0`). NAME is the name you assigned to the connection. MODEMPORT is the device name associated with the port the modem is connected to (in this case, COM1). LINESPEED sets the speed, in bps, between the computer and the modem (not the dial-up speed, which is typically slower). PAPNAME is the user name that you log in with, assuming you are using PAP authentication.

ONBOOT is set to yes to start the `pppd` daemon at boot time (but not dial out yet, since DEMAND=yes is set). DEFROUTE=yes sets the default route to be this PPP connection. DEMAND=yes causes the link to be initiated only when traffic is present. IDLETIMEOUT=600 causes your connection to time out after 600 seconds of being idle (that is, ten minutes).

> **TIP:** If you want to see the exact options set by each of these parameters, look at the contents of the /etc/sysconfig/network-scripts/ifup-ppp script. For example, if DEFROUTE=yes, then the option defaultroute is sent to the pppd daemon. See the pppd man page for a description of each option (type man pppd).

You can add a PPPOPTIONS line to set any additional options you want passed to the pppd daemon process. There are some cases where the ISP will require other values that are not included here. Likewise, there are some options that you should not put in this file when connecting to certain types of servers. Here are some suggestions of values that either should not be in this file or should be (in some cases) for some Windows NT servers. For descriptions of these options, see the pppd man page:

+   * remotename=remotename — You may need this value for PAP authentication, but it should not be entered for CHAP authentication. (For CHAP, the remote PPP server sends you its name.)
+   * require-chap, require-pap, auth, noauth — It’s a nice idea to ask a Windows NT server to authenticate itself (which is what require-chap and require-pap do for their respective protocols). The auth value requires the server to authenticate itself before packets can be sent or received. However, I’m told on good authority that Windows NT will not let you do any of this. Authentication will fail and you will not get a connection. You may need to indicate explicitly that the server is not required to authenticate itself by entering the noauth option.
+   * default-asyncmap — PAP can fail to authenticate because of “link transparency problems.” If authentication fails and you are sure you have the authentication information correct, try adding this value.
+   * ipcp-accept-local, ipcp-accept-remote — Sometimes a server will request your local IP address, even if it wants to assign one itself. The same is true of the remote address. Try adding these lines to the options file:

```
192.168.0.1:192.168.0.2
ipcp-accept-local
ipcp-accept-remote
demand
```