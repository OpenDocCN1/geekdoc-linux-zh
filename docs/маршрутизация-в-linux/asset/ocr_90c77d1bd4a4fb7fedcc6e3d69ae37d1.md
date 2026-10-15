Remote access servers provide support for multiple protocols, with IP being a favorite, although IPX is also found in legacy Novell environments. Although the remote access server provides protocol, interface, and security policy, the remote access server does not typically store user-specific information locally, but rather the user specific-information such as authentication, packet filtering, and protocols available to the user, are determined through a remote access server protocol such as Remote Access Dial In User Service (RADIUS) as defined in RFC 2058. Linux makes an ideal RADIUS server. Table 12.5 lists some RADIUS servers that run on Linux.

# Table 12.5 RADIUS for Linux

| RADIUS | Organization | Source |
|---|---|---|
| Ascend RADIUS version 970224 | Lucent | ftp://ftp.ascend.com/pub/Software-Releases/Radius |
| Cistron Radius Server version 1.6.4 | Cistron Telecom | http://www.radius.cistron.nl/ |
| Livingston Radius Server | Lucent | http://www.livingston.com:80/tech/docs/radius/ftp://ftp.livingston.com/pub/radius/ |

This section has covered traditional remote access, but the recent broadband offerings, such as cable modems and digital subscriber line (DSL), have opened new opportunities for personal and business users. Cable modems and DSL are covered in the next two sections.

# Cable Modems

Cable television networks, outside of the public switched telephone network, are likely the most common networks used by home users. This marketing aspect combined with the infrastructure to create broadband cable networks is an excellent combination for data networking applications.

The cable modem is the hardware used to connect to the Internet through the cable provider's network. Traditional cable networks were uni-directional by nature, and data networking is bi-directional; however, cable providers have long needed the capability to transmit upstream information to provide additional services based upon conventional cable technology, such as pay-per-view. The bandwidth and technology designed to provide this upstream channel is what allows cable networks to provide an