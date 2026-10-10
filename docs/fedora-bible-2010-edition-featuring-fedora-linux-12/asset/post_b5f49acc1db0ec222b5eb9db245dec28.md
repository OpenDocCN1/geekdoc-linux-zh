
## You can use telnet to access the server.

OpenVPN includes TUN/TAP virtual network interface drivers at the networking layer, with device names like /dev/tunX and /dev/tapX. Applications can use the TUN devices as a virtual point-to-point interface to VPN partner (routed mode). TAP devices provide a virtual Ethernet adapter, so daemons listening on TAP can capture Ethernet frames.

The OpenVPN procedure in this chapter describes how to set up an OpenVPN server. This includes:

- Setting up information needed to create certificate authority certificates and keys. In the process you create a root RSA Private Key (ca.key) that you need to keep confidential and a root certificate (ca.crt) that you share.
- Setting up configuration files and starting the OpenVPN service.

To use OpenVPN in Fedora, you need have the openvpn package installed. If it is not yet installed, type:

```bash
# yum install openvpn
```

### Decisions before configuring OpenVPN

The decisions you need to make before setting up your OpenVPN connection include the following:

- **Do you want a public key infrastructure or static key?** If you have a single VPN client connection to a single server, you can use a static key. That way, you don’t have to maintain a key infrastructure. See the OpenVPN HOWTO for more information: [http://openvpn.net/index.php/documentation/howto.html](http://openvpn.net/index.php/documentation/howto.html)
- **Will your VPN do routing or bridging?** Routing, where data are routed from the VPN server to the LAN (instead of just being passed through), is usually a better choice than bridging. Routing is easier to set up and provides more control for specific client features.

The following assumes you decided to set up a public key infrastructure and are using a routing OpenVPN server. For information on using OpenVPN to do bridging, refer to the OpenVPN FAQ (http://openvpn.net/index.php/open-source/faq.html).

### Create a public key infrastructure

Using certificates and private keys, you can create a safe environment for allowing multiple clients to access your private networks over the Internet. The following procedure is done on a Fedora system that doesn't necessarily have to be the same one that you use for your VPN server. In this example, however, the entire procedure is run on the OpenVPN server.

To begin setting up your public key infrastructure, open a Terminal window as root and do the following:

1. **Copy the sample configuration files:**

```bash
# cp -r /usr/share/openvpn/easy-rsa/ /etc/openvpn/
# cd /etc/openvpn/easy-rsa/2.0
```

2. **Choose variables:** Edit the vars file (in this example, the vars file is located in `/etc/openvpn/easy-rsa/2.0`). Most of the defaults will work, as long as you work from this configuration directory. However, you need at least to set the key values that are placed in your certificate. Replace the examples in quotes with your own values:

```bash
export KEY_COUNTRY="US"
export KEY_PROVINCE="WI"
export KEY_CITY="Madison"
export KEY_ORG="Reedsburg-LOG"
export KEY_EMAIL="chris@linuxtoys.net"
```

In the vars file, you can also change such values as the default key size (1024) and days to certificate expiration (3650 days).

3. **Set variables:** Export the variables in the vars file to the current shell so they can be used by the later commands you run:

```bash
# source ./vars
```

4. **Prepare to create new keys:** If there are any keys in your KEY_DIR (probably named keys/ in the current directory), this command removes them and creates index.txt and serial files in that directory:

```bash
# ./clean-all
```

Next you will create the server certificates and keys.

5. **Build root certificate authority certificate and key:** Run the following script, which in turn will use the pkitool command to create a 1024-bit RSA private key:

```bash
# ./build-ca
Generating a 1024 bit RSA private key
...
writing new private key to 'ca.key'
```

The interaction output is as follows:

```text
Country Name (2 letter code) [US]:
State or Province Name (full name) [WI]:
Locality Name (eg, city) [Madison]:
Organization Name (eg, company) [Reedsburg-LOG]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) [Reedsburg-LOG CA]:
Email Address [chris@linuxtoys.net]:
```

You should have two new files in the keys directory. The ca.key file holds the private key and the ca.crt key holds the new certificate generated from your KEYS values.

6. **Create parameters for SSL/TLS:** Type the following to build the server-side Diffie-Hellman parameters needed for SSL/TLS connection:

```bash
# ./build-dh
Generating DH parameters, 1024 bit long safe prime, generator 2
This is going to take a long time
......+....+............................+
```

This creates a file named dh1024.pem in the keys directory.

7. **Create server keys and certificates:** Run the following command to create the keys and certificates needed on the OpenVPN server, replacing *server1* with your server's hostname or other common name to identify it:

```bash
# ./build-key-server server1
Generating a 1024 bit RSA private key
..+++++
...................................................................+++++
writing new private key to 'server1.key'
.
.
A challenge password []: chzypassw77
An optional company name []:
Using configuration from /etc/openvpn/easy-rsa/2.0/openssl.cnf
.
.
Sign the certificate? [y/n]::y
1 out of 1 certificate requests certified, commit? [y/n]   y
Write out database with 1 new entries
Data Base Updated
```

The command just run produces the *server1.crt*, *server1.csr*, and *server1.key* files in the *keys* directory. The *server1.key* file must be kept secret! Next you need to create client certificates and keys for each client you want to connect to your OpenVPN server.

8. **Create client certificates and keys:** Run the *build-key* (or *build-key-pass*) script for every client that you want to use the OpenVPN server. Here are examples running the *build-key* script for two clients, named *client01* and *client02*:

```bash
# ./build-key client01
.
.
A challenge password []: my67ChvyB
An optional company name []:
Sign the certificate? [y/n] y
1 out of 1 certificate requests certified, commit? [y/n]  y

# ./build-key client02
.
.
.
```

After you have run *build-key* for every client, you will have a *crt* (*client01.crt*), *csr* (*client01.csr*), and *key* (*client01.key*) file in the *keys*/ directory for each client. The next step is to make sure each of those keys is transported to the appropriate computer.

For this example, we will copy the keys to a directory on the Fedora client machine we are calling *client01* in the */etc/openvpn/keys/* directory on that machine. (See the section “Create OpenVPN client configuration” later in this chapter.)

### Create OpenVPN server configuration

Before starting the OpenVPN service on the server, you need to create a *server.conf* file in the */etc/openvpn* directory. You can do this by copying a sample *server.conf* file and editing it. Here is an example of one you can use:

```bash
# cd /usr/share/doc/openvpn-2.1/sample-config-files
# cp server.conf /etc/openvpn/
```

As root user, open the *server.conf* file in any text editor. This is an example for a multi-client server that is doing routing (not bridging). The locations of key files should match those you created earlier in this section. (Many of the comments have been left out of this example, but you should read them in the *server.conf* file to guide your configuration.)

```nginx
port 1194
proto udp
dev tun
ca /etc/openvpn/easy-rsa/2.0/keys/ca.crt
cert /etc/openvpn/easy-rsa/2.0/keys/server1.crt
key /etc/openvpn/easy-rsa/2.0/keys/server1.key # This file should be kept secret
dh /etc/openvpn/easy-rsa/2.0/keys/dh1024.pem

server 10.8.0.0 255.255.255.0

keepalive 10 120
comp-lzo

persist-key
persist-tun

status openvpn-status.log

verb 3
```

In this configuration, the OpenVPN server listens on port 1194, UDP protocol, as a routing VPN server (dev tun). You can use a different port number, to make the service more obscure, but the clients must use that port number as well. The private network that OpenVPN clients will be able to reach from this VPN connection is on the subnetwork 10.8.0 (identified by 10.8.0.0 255.255.255.0). With the configuration file completed, you can start the OpenVPN service on the server by typing the following:

```bash
# service openvpn start
```

The last step you need to do to make your OpenVPN server ready to accept connections is to open your firewall to accept connections on port 1194 and to allow your system to route packets for your private subnetwork. In this example, we used a private subnetwork with IP addresses of 10.8.0.1 through 10.8.0.254. See the “Securing Linux with the iptables Firewall” section of Chapter 13 for details.

### Create OpenVPN client configuration

To configure an OpenVPN client to connect to the OpenVPN server you just configured, you need to copy the key files to the client, create a client configuration file, and start the service. Here is an example of how you might copy the keys from the server:

```bash
# cd /etc/openvpn
# mkdir keys
# scp root@server1:/etc/openvpn/easy-rsa/2.0/keys/ca.crt keys
# scp root@server1:/etc/openvpn/easy-rsa/2.0/keys/client01.crt keys
# scp root@server1:/etc/openvpn/easy-rsa/2.0/keys/client01.key keys
```
