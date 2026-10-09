# # PPP

The Point-to-Point Protocol (PPP) goes beyond the simple encapsulation protocol used by SLIP. The Link Control Protocol (LCP) used in PPP can encapsulate and multiplex multiprotocol datagrams. PPP also provides additional session negotiation options, link-level error detection, compression, and authentication.

PPP is a subsystem managed by the system resource controller. The primary PPP control daemon pppcontrol is started as a subprocess and is responsible for loading the PPP kernel extensions. One ppptad subscriber is started for each PPP connection. ppptach binds the PPP and TTY STREAM. Configuration information for the PPP subsystem is stored in the `/etc/ppp` directory.

PPP uses both PAP (Password Authentication Protocol) and CHAP (Challenge Handshake Authentication Protocol) as authentication methods for the client machines to authenticate to the server machines. The differences between them are that in PAP, the client name and password (shared secret) are sent in clear text, while in CHAP, the shared secret is not sent in clear text. Instead, the server sends a challenge, and the client must prove that it knows the secret by generating a hash value from the challenge and the shared secret and sending the value to the server. The server also generates its own hash value and compares with the value received from the client.

To configure the PPP subsystem, begin by invoking the SMIT FastPath smitppp. The first step will be to configure LCP (see Figure 13-9). You will need to choose a subsystem name for LCP. This can be any text string. It is not related to any TCP name service entry. Next, define the maximum number of server (inbound connections), client (outbound connections), and demand (sessions started when network traffic is detected) connections to be supported by LCP. You can throttle the mixture of server, client, and demand connections by the maximum number of IP interfaces and asynchronous high-level data link control (HDLC) attachments defined for the subsystem.

```
```
# smit pppicp
```
```

Once the LCP subsystem is defined, you will need to set the IP addresses to be used when PPP connections are established. Invoke the SMIT FastPath smit pppip (see Figure 13-10). Identify the local machine's IP address, the base IP number for assigned addresses, the number of addresses to be assigned, and the subnet mask.

```
```
# smit pppip
```
```

If you chose to use authentication for establishing connections, invoke the SMIT FastPath smit ppppap or smit ppchap. Add each user, machine, and password that will be allowed to establish a PPP connection. These values are stored in clear text in the /etc/ppp/ppp-secrets file. Verify that permissions restrict access to this file.

When configuration has been completed, you can start the PPP subsystem using SMIT or the startrc -p spp command.

```
```
# startrc -p spp    # Start PPP subsystem
```
```