For an added twist, you may have your VPN server set up to accept dial-in connections so that you do not have to go through the Internet at all.

The point to make with this example is that you, the user, must do something such as start a program on the laptop to initiate a VPN connection. If it's a Linux-based laptop, you may need to start IPsec services using a script after you are connected to the Internet.

# ## Connecting Networks

Let’s contrast the preceding case with the case in which you want to connect two networks. These networks could be in separate physical locations, or they could just be two separate subnets of the same network.

In this configuration, the VPN gateways have startup scripts to start IPsec services at boot time. The servers establish a secure connection with each other. Both gateways have a static route to the other gateway. From a user perspective, they don’t need to do anything to communicate and share information between networks. All communication is taken care of by the VPN gateways. From the perspective of the user, it looks as though Network 2 is on the same network as Network 1. This may be a slight oversimplification, of course, but that is essentially what happens.

> **AUTHENTICATION**
> 
> It’s important to note that, in both of these configurations, the user is not being authenticated. Instead, the computer that the VPN software is running on is authenticated. This is particularly noticeable in the dual-network configuration. Here the gateways know about each other and authenticate traffic coming from the other. This process differs greatly from the traditional client/server thinking and technology we have today.

You can set up a lot more complex configurations than those shown here. However, they all have similarities. All VPN gateways know about and have routes to the other VPN gateways in any configuration. Authentication occurs at the gateway level, not the user level.

# ## VPN and Firewalls

A VPN can be placed in front of a firewall, be placed behind a firewall, or be part of a firewall implementation. Placing the VPN in front of a firewall is not very common. It is more common to use a firewall/VPN combo or to put the VPN behind the firewall itself.