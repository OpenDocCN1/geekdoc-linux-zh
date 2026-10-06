# Chapter 7

# Virtual Private Networks

# Chapter Objectives

After reading this chapter and completing the exercises, you will be able to do the following:

+   - Use a virtual private network (VPN).
- Use Point-to-Point Tunneling Protocol (PPTP) as an encryption tool for VPNs.
- Use Layer 2 Tunneling Protocol (L2TP) as an encryption tool for VPNs.
- Add security and privacy to a communication using IPSec.
- Understand and evaluate VPN solutions.

# Introduction

Earlier chapters focus primarily on security within a network. However, what happens when remote users want to log on to a network versus simply accessing a web server or FTP server on the network? This process involves a remote user, perhaps an remote office, connecting to the network and accessing resources as if she were on your local network. This clearly presents significant security issues.

Virtual private networks (VPNs) are becoming a common way to connect to a network in a secure session. A VPN creates a private network connection over the Internet to connect remote sites or users together. Instead of using a dedicated connection such as leased lines, a VPN uses virtual connections routed through the Internet from the remote site or to the private network. Security is accomplished by encrypting all the transmissions.

A VPN allows a remote user to have network access just if she were local to the private network. This means not only connecting to the network as if she were local but also making the connection secure. Because most organizations have many employees traveling and working from home, remote