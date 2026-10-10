![](bbox=[0.17, 0.07, 0.67, 0.45])

Figure 4.6 shows the host-key database for SSH Communications' SSH client. Similar to SecureCRT, this is the repository for the SSH client for all host keys obtained after a connection is made to a SSH server. This host-key database will be referenced each time the SSH client connects to the same SSH server to make sure the host keys match.

# # Public Keys

Public-key authentication is one of the best authentication methods provided by SSH. Unlike password authentication, public-key authentication requires each user to contain a public-key file in order to authenticate. The fact that many corporate networks rely on user passwords, no matter how strong or weak, to protect sensitive and proprietary information leaves many networks vulnerable to simple attacks. The following sidebar provides several reasons why using passwords on sensitive systems may not be the best decision in order to attain an acceptable level of security: