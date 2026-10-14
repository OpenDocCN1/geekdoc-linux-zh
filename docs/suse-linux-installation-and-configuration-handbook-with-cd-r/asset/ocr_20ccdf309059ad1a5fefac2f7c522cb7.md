The file smb.conf has some special sections:

+   - `global`
+   - `homes`
+   - `printers`

# The global Section

As stated earlier, this section contains all the basic configuration parameters that apply to Samba. You have already seen three of them—the workgroup, server string, and security. Let's look at some other parameters you can use.

# The netbios name Parameter

As you have seen, Samba by default uses your machine's hostname as its network name. You easily can change this behavior by using the netbios name parameter. To call your machine SuSELinux for example, you would add `netbios name = SuSELinux` to the global section of your smb.conf file. As you will see later, this option can be used in other, more advanced ways.

# The keep alive Parameter

When a client machine connects to a Samba server, an open connection is established, which consumes resources. If the client machine crashes, this connection remains open. It can take Samba a considerable length of time before it finds out that this open connection is not actually being used, which wastes more resources. To force Samba to check on its clients, set `keep alive = 30`.

# The security Parameter

This option defines the security used by Samba. As you saw earlier, when this option was not set, Samba defaulted to user security, forcing the connecting clients to enter a password to use the server. Setting this option to share allows anyone to browse the machine. As will be discussed later, you can have a mixture of both—needing a password and not needing one.

# The interfaces Parameter

This parameter tells Samba which networking interface to use. By default, Samba uses all the available interfaces on the machine. You won't really need this option if you have just one interface, for example an Ethernet card. But, if you have more than one, and you don't want Samba to listen on all of them, you can force it to listen to just the ones you want. To use this parameter, you need to give it the IP and netmask of the interfaces to use. Use a space as a separator between the different interfaces. The final form of the parameter is `interfaces = xxx.xxx.xxx.xxx/xxx.xxx.xxx.xxx xxx.xxx.xxx.xxx/xxx.xxx`. The following is an example:

`interfaces = 192.168.17.17/255.255.255.0`

# The hosts allow and hosts deny Parameters

You can use these options to control which machines can connect to your Samba server. For example, to allow all machines to connect to your server except for those that come from the subnet 192.168.121, you would enter `hosts allow = ALL EXCEPT 192.168.121..` This will deny access to any machine coming from that