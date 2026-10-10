```
1 out of 1 certificate requests certified, commit? [y/n]  y
   # .//build-key client02
```

After you have run build-key for every client, you will have a crt (client01.crt), csr (client01.csr), and key (client01.key) file in the keys directory for each client. The next step is to make sure each of those keys is transported to the appropriate computer.

For this example, we will copy the keys to a directory on the CentOS client machine we are calling client01 in the /etc/openvpn/keys/ directory on that machine. (See the “Create OpenVPN Client Configuration” section later in this chapter.)

# Create OpenVPN Server Configuration

Before starting the OpenVPN service on the server, you need to create a server.conf file in the /etc/openvpn directory. You can do this by copying a sample server.conf file and editing it. Here is an example of one you can use:

```
# cd /usr/share/doc/openvpn-2.0.9/sample-config-files
# cp server.conf /etc/openvpn/
```

As root user, open the server.conf file in any text editor. This is an example for a multi-client server that is doing routing (not bridging). The locations of key files should match those you created in the key server section earlier. Many of the comments have been left out of this example, although you should read them in the server.conf file to guide your configuration.

```
port 1194
proto udp
dev tun

ca /etc/openvpn/easy-rsa/2.0/keys/ca.crt
 cert /etc/openvpn/easy-rsa/2.0/keys/server.crt
 key /etc/openvpn/easy-rsa/2.0/keys/server.key       # This file should be kept secret
 dh /etc/openvpn/easy-rsa/2.0/keys/dh1024.pem

server 10.8.0.0 255.255.255.0

keepalive 10 120
comp-lzo

persist-key
persist-tun
```