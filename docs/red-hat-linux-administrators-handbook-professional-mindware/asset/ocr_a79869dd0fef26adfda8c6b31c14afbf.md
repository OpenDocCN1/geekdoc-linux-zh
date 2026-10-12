# Chapter 16

# Network Security

# Designing a Secure Network

As a network grows, implementing security as an afterthought becomes more difficult. Users grow accustomed to patterns of usage, poor choices become accepted handicaps, and the administrator must play political games to make changes. These are some of the reasons security of your network as a whole must be examined as you plan the topology.

# Using private IP addresses

The simplest way to maintain security on a network is to ensure that hosts on your network cannot contact, nor be contacted by, the outside world. The easiest way to achieve this would be to never connect them to a public network such as the Internet. However, this security-through-isolation strategy is not practical in many situations. Using private IP addresses is an easy way of allowing your users to reach the Internet while holding off the miscreants from getting to the user machines.

RFC 1918 specifies blocks of IP addresses that may be used within a local TCP/IP network but may not traverse Internet routers. These groups of IP addresses are commonly called LAN IP addresses or private IP addresses. Because these IP addresses do not route across the Internet, you do not need to register to use them. By assigning an IP address from within this range, you effectively limit traffic to and from the computer to the local network. This is a quick and effective way of denying outside access to computers while allowing traffic to flow among your internal computers.