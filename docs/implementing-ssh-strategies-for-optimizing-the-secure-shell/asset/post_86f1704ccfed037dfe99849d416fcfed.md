
6. To show and confirm the configuration results of the SSH server, enter the following commands:

```
Router# show ip ssh

SSH Enabled - version 1.5
Authentication timeout: 120 seconds; Authentication retries: 3
```

7. To view the SSH session, enter the following command:

```
Router# show ssh
```

This command shows any connections that are established, the version, the encryption, the state, and the username.

8. Once SSH is enabled and configured, it may be appropriate to prevent any non-SSH connections to access the router, such as Telnet. It is important to disable insecure protocols such as Telnet if a stronger and more secure protocol is in place and provides the same type of access.

To require the use of SSH on terminal-line connections, enter the following command:

```
Router(config)# line vty 0 4
Router(config-line)# transport input ssh
```

9. Once SSH has been enabled on the Cisco router, enter the following commands to connect to the SSH service on the router:

Syntax:
`ssh -1 userid -c <des | 3des> -p <port number> IP.Address/hostname`

Example:
`ssh -1 <username> -c 3des <router_ip.address>`

In addition to providing SSH access to a router, Cisco IOS provides terminal-line access with SSH, which allows SSH access to non-SSH routers that have a console or serial-port connection to an SSH-enabled router. A simple terminal-line access configuration is illustrated in Figure 5.1.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_186_0.png)

To set up terminal-line SSH access, each line must be configured with its own rotary, and SSH must be configured to use SSH when accessing the other devices. The following steps walk you through this process.

1. Each line must be configured on the SSH-enabled router. Note that the line number refers to the port number on the remote SSH server. For example, line number 1 equates to port 2001, line number 2 equates to port 2002, and line number 3 equates to port 2003. The following syntax shows the router commands to enter a line number for SSH.
   Syntax:
   `Router(config)# line <line-number> <ending-line-number>`
   Example:
   `Router(config)# line 1 200`

2. Disable the EXEC process of each line using the following syntax:
   `Router(config)# no exec`

3. Define the login authentication option, which must be username/password, with the following syntax:
   Syntax:
   `Router(config)# login authentication <listname>`
   Example:
   `Router(config)# login authentication default`

4. Define a group of lines that will be used when SSH is enabled using the following syntax:
   Syntax:
   `Router(config)# rotary <group>`
   Example:
   `Router(config)# rotary 1`

5. Define the use of SSH on the line using the transport input command, as listed:
   `Router(config)# transport input ssh`

6. Configure SSH for the TTY lines, the port number to connect to, and the rotary group using the following syntax:
   Syntax:
   `Router(config)# ip ssh port <portnumber> rotary <group>`
   Example:
   `Router(config)# ip ssh port 2001 rotary 1`

7. SSH terminal-line access should now be configured! Any SSH client connection to the SSH-enabled router on port 2001 should be given access to the non-SSH enabled router via the serial-line or console to the SSH-enabled router.

Once SSH has been enabled on the Cisco router, enter the following commands to connect to the remote router via the serial-line:
`ssh -c 3des -p 2001 <router.ip.address>`

## Cisco Switches

Cisco Catalyst Operating System (CatOS) started to support the use of SSH from version 6.1. Since then, CatOS 6.1 and up has supported SSH version 1 only. While the use of SSH version 1 still has its insecurities, the replacement of Telnet on Cisco devices has added a tremendous amount of security to the network device. SSH is supported on the following Cisco switches: Catalyst 3550, 4000, 5000, 6000, 8540, and 8510.

To use SSH on Cisco routers, complete the following steps.

1. Download the correct CatOS to the switch. Make sure you are downloading a CatOS version that holds SSH support. Cisco SSH servers require the IPsec (DES or 3DES) encryption software image from CatOS 6.1.

2. Generate the RSA Key with the following command:
   ```
   Cat6509> (enable) set crypto key rsa 1024
   ```

3. Restrict SSH to authorized host/subnets with the following commands:
   ```
   Cat6509> set ip permit 172.16.1.0 255.255.255.0
   ```

4. After the key hash has been made, enable SSH with the following command:
   ```
   Cat6509> (enable) set ip permit enable ssh
   ```

5. Once SSH has been enabled on the Catalyst switch, enter the following command to connect to the SSH services on the switch:
   ```
   ssh -C 3des -v <switch ip address>
   ```

## Cisco VPN Concentrator

Cisco’s VPN device, the VPN concentrator, comes with SSH operability out-of-the-box. There is no need to load software on the VPN concentrator similar to the routers and the switches. To view the SSH options on the concentrator, browse to your VPN device with any Web browser, preferably over SSL. If SSL is not enabled, consider consoling into the VPN device, but do not use clear-text protocols such as HTTP over insecure networks such as the Internet. Once you have authenticated to the Configuration screen, browse to System Management Protocols SSH. You should see a configuration screen similar to Figure 5.2.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_189_0.png)

**Figure 5.2** The SSH configuration screen of the Cisco VPN concentrator.

Table 5.1 lists and describes the various SSH configuration options available on the configuration screen.

**Table 5.1** VPN Concentrator SSH Configuration Options

| OPTION | DESCRIPTION |
| :--- | :--- |
| Enable SSH | To enable, simply click on Enable SSH checkbox. This box should be enabled by default. |
| SSH Port | Determines the port the SSH service should listen on. The default port is 22; however, any port can be set. |
| Maximum Sessions | Determines the number of simultaneous connections that are allowed. The number can range from 1 to 10, with the default setting to 4. |
| Key Regeneration Period | Sets the time interval to regenerate the key, specified in minutes. The range can be between 0, which disables key regeneration, and 10080, which is up to one week. The default setting is 60 minutes. |
| Encryption Protocols | Specifies which algorithms should be used to negotiate the SSH session between the clients and the VPN concentrator. Possible options are 3DES-168-bit key, RC4-128-bit key, DES-56-bit key, and No entry. Unselecting all options disables SSH, and choosing No Entry provides no encryption whatsoever. As best practices, select 3DES-168-bit key and RC4-128-bit key. |

After the SSH options have been set, select the Apply button to apply the settings. SSH should now be enabled on the VPN concentrator on port 22 with the following settings:

- SSH Port—22
- Maximum Sessions—4
- Key Regeneration Period—45
- Encryption Protocols—3DES-168 and RC4-128

## Cisco PIX Firewalls

Cisco PIX firewalls started to support the use of SSH from version 5.2. Since then, PIX versions 5.2 and above have supported SSH version 1 only. While the use of SSH version 1 still has its insecurities, the replacement of Telnet on Cisco firewalls has added a tremendous amount of security to the network device.

To use SSH on Cisco firewalls, complete the following steps:

1. Download the correct PIX version to the firewall. Make sure you are downloading a PIX version that holds SSH support. Cisco SSH servers require IPsec (DES or 3DES) encryption software image from version 5.2.

2. Make sure a hostname and host domain have been configured for the router. These are not SSH commands but are required in order to use SSH. The following information needs to be entered:
   ```
   Syntax: Pix# hostname <hostname>
   Example: Pix# hostname Pix-Firewall
   ```
   ```
   Syntax: Pix# domain-name <domainname>
   Example: Pix# domain-name Aum.com
   ```

3. Generate an RSA key pair for the firewall and save it with the following commands:
   ```
   Pix# ca generate rsa key 1024
   Pix# CA save all
   ```

4. Select the interface on the firewall to use SSH. Most likely, this will be the internal interface. The internal interface is called inside with an RFC 1918 address, as shown with the following syntax:
   ```
   Pix# ssh 172.16.1.1 255.255.255.255 inside
   ```

5. Set the authentication timeout for SSH. The maximum timeout cannot exceed 120 seconds, which is also the default; however, once the session
