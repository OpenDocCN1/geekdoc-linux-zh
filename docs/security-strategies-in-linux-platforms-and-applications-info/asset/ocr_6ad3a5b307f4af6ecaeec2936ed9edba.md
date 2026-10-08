# # Protect Your Time Services

Time services on Linux rely on the NTP protocol. Basic information on NTP server configuration was covered in Chapter 8. This section goes further, describing those directives in the /etc/ntp.conf file that can secure a local NTP server. If an NTP server is overloaded by any, it may not be a security issue per se. However, it affects the reliability of the time from that server, it can have other consequences. For example, if the NTP server of an inventory system is not synchronized to the NTP server of a sales system, customers may try to order products that are out of stock.

The security-related directive in this file is restrict. Take a look at the directive as configured in the default ntp.conf file. The -4 and -6 correspond to IPv4 and IPv6

```
restrict -4 default kod notrap notify nopeer noquery
restrict -6 kod notrap notify nopeer noquery
```

The other options affect security of the NTP server in the following ways:
* default—Access to all NTP clients is allowed by default.
* kod—Prevents attacks from kiss of death (KOD) packets.
* notrap—Prevents access to the trap service for logging.
* modifyify—Prevents other NTP servers from modifying the status of this server.
* nopeer—Disallows attachments from other NTP servers.
* noquery—Disallows queries of the NTP service.

Assuming you don't want to open this up as a public NTP server, the default option should not be used. However, some address is required; one option is the IP address of the local network. In addition, you may want to allow time queries, and allow other NTP servers, perhaps from remote networks administered by colleagues, to communicate with your NTP server. The IPv4 restrict directive would change to the following:

```
restrict -4 192.168.0.0 mask 255.255.255.0 kod notrap modify
```

In a similar fashion, you could set up restrictions on the IPv6 network:

```
restrict -6 0011:838:0:1:: mask fffff:ffff:ffff:
---> kod notrap modify
```

# # Options for Obscurity: Different Ports, Alternative Services

To some extent, when you installed Linux, you made a choice for obscurity. But as you've seen so far in this book, obscurity can mean different things when applied to different services. Obscurity goes beyond the use of nonstandard ports for network communications.