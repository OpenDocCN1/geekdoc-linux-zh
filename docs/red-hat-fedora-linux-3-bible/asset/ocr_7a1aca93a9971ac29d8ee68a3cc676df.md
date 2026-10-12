CAUTION: The pap-secrets and chap-secrets files should not be accessible by anyone but the root user. Anyone gaining this information could use it to access your Internet account. By default, permissions are closed to all but the root user. (To close permission, type chmod 600 /etc/ppp/*secrets.)

# Looking at the ifcfg-ppp0 file

The ifcfg-ppp0 file (/etc/sysconfig/network-scripts/ifcfg-ppp0) contains options that are passed to the pppd daemon for features that are negotiated with the remote PPP server. Most of the problems that can occur with your PPP connection result from getting some of the options wrong (particularly asking for features the server can't or won't provide).

Here is an example of the ifcfg-ppp0 file used to connect to a Windows NT PPP server:

```
DEVICE=ppp0
NAME=Acme_Internet_Service
MODEMPORT=/dev/ttyS0
LINESPEED=115200
PAPNAME=guest
ONBOOT=yes
DEFROUTE=yes
DEMAND=yes
IDLETIMEOUT=600
```

The device name is ppp0 (which is associated with the configuration file ifcfg-ppp0). NAME is the name you assigned to the connection. MODEMPORT is the device name associated with the port the modem is connected to (in this case, COM1). LINESPEED sets the speed, in bps, between the computer and the modem (not the dial-up speed, which is typically slower). PAPNAME is the user name that you log in with, assuming you are using PAP authentication.

+   * ONBOOT is set to yes to start the pppd daemon at boot time (but not dial out yet, since DEMAND=yes is set). DEFROUTE=yes sets the default route to be this PPP connection.
+   * DEMAND=yes causes the link to be initiated only when traffic is present. IDLETIMEOUT=600 causes your connection to time out after 600 seconds of being idle.

TIP: If you want to see the exact options set by each of these parameters, look at the contents of the /etc/sysconfig/network-scripts/ifup-ppp script. For example, if DEFROUTE=yes, then the option defaultroute is sent to the pppd daemon. See the pppd man page for a description of each option (type man pppd).

You can add a PPOPTIONS line to set any additional options you want passed to the pppd daemon process. There are some cases where the ISP will require other values that are not included here. Likewise, there are some options that you should not put in this file when connecting to certain types of servers. Here are some suggestions of values that either should not be in this file or should be (in some cases) for some some Windows NT servers. For descriptions of these options, see the pppd man page: