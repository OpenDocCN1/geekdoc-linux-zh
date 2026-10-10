# Cisco Switches

Cisco Catalyst Operating System (CatOS) started to support the use of SSH from version 6.1. Since then, CatOS 6.1 and up has supported SSH version 1 only. While the use of SSH version 1 still has its insecurities, the replacement of Telnet on Cisco devices has added a tremendous amount of security to the network device. SSH is supported on the following Cisco switches: Catalyst 3550, 4000, 5000, 6000, 8540, and 8510.

To use SSH on Cisco routers, complete the following steps.

+   Download the correct CatOS to the switch. Make sure you are down-\  loading a CatOS version that holds SSH support. Cisco SSH servers\  require the IPsec (DES or 3DES) encryption software image from\  CatOS 6.1.

2. Generate the RSA Key with the following command:

```
Cat6509> (enable) set crypto key rsa 1024
```

3. Restrict SSH to authorized host/subnets with the following commands:

```
Cat6509> set ip permit 172.16.1.0 255.255.255.0
```

4. After the key hash has been made, enable SSH with the following\  command:

```
Cat6509> (enable) set ip permit enable ssh
```

5. Once SSH has been enabled on the Catalyst switch, enter the following\  command to connect to the SSH services on the switch:

```
ssh -C 3des -v <switch ip address>
```

# Cisco VPN Concentrator

Cisco’s VPN device, the VPN concentrator, comes with SSH operability out-of-\  the-box. There is no need to load software on the VPN concentrator similar to\  the routers and the switches. To view the SSH options on the concentrator,\  browse to your VPN device with any Web browser, preferably over SSL. If SSL\  is not enabled, consider consoling into the VPN device, but do not use clear-\  text protocols such as HTTP over insecure networks such as the Internet. Once\  you have authenticated to the Configuration screen, browse to System  Mana-\  gement Protocols  SSH. You should see a configuration screen similar to\  Figure 5.2.