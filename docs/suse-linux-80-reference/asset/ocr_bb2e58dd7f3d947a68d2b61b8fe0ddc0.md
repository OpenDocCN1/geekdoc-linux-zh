# Configuring an ADSL or T-DSL Connection

# Default Configuration

Currently, SuSE Linux supports DSL connections that work with the point-to-point over ethernet protocol (PPPoE) used by most major providers. If you are not sure what protocol is used for your DSL connection, ask your provider. If you have a single-user workstation with a graphical interface, the DSL connection should be set up with the YaST2 modules ADSL/T-DSL.

+   1. The ppp and smpppd packages must be installed. It is best to use YaST2 for this purpose.
+   2. Configure your network card with YaST2. Do not activate dhcp, but set a fixed IP address instead, e.g. `192.168.2.22`.
+   3. The parameters set with YaST2 will be saved in the file `/etc/sysconfig/network/providers/dsl-provider0`. In addition, there are configuration files for the SuSE meta ppp daemon and its frontends kinternet and cinternet. Please consult the man page `man smpppd`.
+   4. Start the network with the command `rcnetwork start`.
+   5. With the commands `cinternet --start` and `cinternet --stop` the connection can be established or terminated on a non graphical system and On a graphical desktop use kinternet that is started automatically if you used YaST2 to set up DSL. Click on the gear icon in the control panel. Select ‘Communication/Internet’ → ‘Internet Tools’ → ‘kinternet’. A plug icon will appear in the control panel. Start the connection by clicking on it once and, by clicking on it again, terminate the connection.

# DSL Connection by Dial-on-Demand

Dial-on-demand means that the connection will automatically be set up when the user goes online, for example, when visiting a web site in a browser or when sending an e-mail. After a certain amount of idle time when no data is being sent or received, the connection will automatically be dropped. Since the dial-up connection via PPPoE, the protocol for ADSL, is quite fast, it is almost as if you had an ongoing Internet connection.

However, this really only makes sense if you have a flat-rate connection. If your Internet access is billed by the length of time online, make sure that there are not any interval processes, such as a cronjob, which may be periodically establishing a connection. This could get quite expensive.