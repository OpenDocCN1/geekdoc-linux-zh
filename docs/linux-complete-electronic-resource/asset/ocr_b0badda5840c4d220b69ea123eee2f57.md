You then need to add entries to both your /etc/passwd and your /etc/diphopts files. The entries you need to make are formatted as fol-lows: To configure Linux as a SLIP server with dip, you need to create some special SLIP accounts for users, where dip (in input mode) is used as the login shell. A suggested convention is to have all SLIP accounts begin with a capital "S," e.g. "Sfredm." A sample /etc/passwd entry for a SLIP user looks like:

![](bbox=[0.2, 0.27, 0.9, 0.42])

After the user logs in, the login program, if it finds and verifies the user ok, will execute the diplogin command. dip, when invoked as diplogin, knows that it should automatically assume that it is being used a login shell. When it is started as diplogin the first thing it does is use the getuid( ) function call to get the user ID of whoever has invoked it. It then searches the /etc/diphopts file for the first entry that matches either the user ID or the name of the tty device that the call has come in on and configures itself appropriately. By judicious decision as to whether to give a user an entry in the diphopts file, or whether to let the user be given the default configura-tion you can build your server in such a way that you can have a mix of static and dynamically assigned address users. dip will automatically add a "Proxy-ARP" entry if invoked in input mode, so you do not need to worry about manually adding such entries.

# Configuring /etc/diphopts

/etc/diphopts is used by dip to lookup preset configurations for remote hosts. These remote hosts might be users dialing into your Linux machine, or they might be for machines that you dial into with your Linux machine. The general format for /etc/diphopts is as follows:

```
Suali:::145.71.34.1:145.71.34.2:255.255.255.0:SLIP wa1:t:CSLIP,1006 tyyS1:::145.71.34.3:145.71.34.2:255.255.255.0:Dymanic ttyS1:CSLIP,296
```