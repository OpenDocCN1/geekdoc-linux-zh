
The two preceding approaches provide a fast, easy, inexpensive, and secure solution for wireless networks. While these solutions may not be relevant for all wireless networks or requirements, SSH does solve two of the major requirements for wireless users: secure Web browsing and secure e-mail.

## Summary

The combination of SSH and proxy technology, whether it be HTTP proxies, a SOCKS server, or dynamic port forwarding, gives SSH even more powerful capabilities. The combination of these two technologies allows SSH to be used very easily in insecure and inflexible networks, such as 802.11b wireless networks. Also, with the use of Web proxies or SOCKS, protocols that were very difficult to secure unless large investments in security devices were purchased are now easy to set up at a very low cost.

SSH and SOCKS demonstrate how SOCKS servers combined with SSH flexibility can simplify an SSH architecture while providing end-to-end SSH security. The ability to centralize SSH communications to a single destination, which can then be dispersed to several locations, while providing the use of SSH encryption to/from the entire connection, makes SSH and SOCKS an attractive and simple solution in what could be a complex architecture.

Furthermore, the use of dynamic port forwarding, which creates a fully functional SOCKS server on the local SSH client, adds an incredible amount of flexibility to SSH. Since the use of dynamic port forwarding allows SSH clients to have the benefit of SOCKS technology, or even proxy technology, without the use of a secondary proxy or SOCKS server, it is a very attractive solution that is not only easy to implement (with the need for just a single flag on a supporting SSH client), but easy to support as well (by requiring only a default SSH server without extra configuration or plug-ins). The ability to secure Web, FTP, and mail applications with a single port-forwarding rule without changing any aspects of the SSH server or the architecture it rides in makes dynamic port forwarding a very strong feature of SSH.

The ability to use HTTP proxies with SSH allows SSH secure Web communication from insecure networks through a relatively easy process. Many organizations have deployed proxy servers probably for other reasons; however, with the use of local port forwarding, the existing proxy servers can be used to port forward local connections over secure tunnels to an existing (or new) internal proxy server. This combination allows external employees, such as employees who work from home or travel considerably, to use trusted internal servers for sensitive communications, such as financial applications that are only Web enabled.

Lastly, this chapter briefly describes how to use SSH technologies with HTTP proxies and dynamic port forwarding to secure 802.11b wireless networks. The details learned from the previous section of this chapter can be used not only in traditional wired networks but also in newly emerging networks with strong security issues, such as wireless ones. While wireless and SSH do have scalability draw-backs, SSH can secure a wireless network with relatively low overhead, low cost, and high performance without the need to redesign any type of network or network segment.

The next chapter provides a discussion of SSH case studies. This chapter provides various real-world examples on how SSH can be used to solve several critical functionality and security issues within an organization. Furthermore, the chapter will discuss many of the key aspects, features, and functions discussed in the previous chapters, while highlighting the most powerful and useful functions.

# CHAPTER 10

## SSH Case Studies

When Trinity needed to hack into the Zion mainframe in order to save the world in the motion picture Matrix Reloaded, what utility does she use? That's right, she uses SSH. If this book has shown you one thing, it should be that not only can SSH be used to save the world; it should be regarded as a gift from the gods. Seriously, while Trinity demonstrates one of the many benefits of SSH, which is secure terminal access to a mainframe system, the most important aim of this book is to demonstrate the flexibility of SSH when properly optimized.

In order to fully demonstrate SSH's flexibility, let's examine three case studies in this chapter. These are real-world situations in which SSH is used to significantly improve the functionality and/or the security of a particular architecture. The following are the three case studies:

- Secure remote access
- Secure wireless connectivity
- Secure file servers

Each case study consists of the following four items:

- A problem
- Business requirements
- Configuration
- Results checklist

### Case Study # 1: Secure Remote Access

The following case study involves the Ace Tomato Company. The Ace Tomato Company is a multinational organization headquartered in Mumbai, India, that produces and sells dairy milk all over the world. It has sales, professional services, and technical-support divisions that travel to customer sites 90 percent of the time, which is either outside of the country, primarily in the Nashville, TN, Columbus, OH, Brookings, SD, Minneapolis, MN, and San Francisco, CA, or locally around the country, primarily in Belwa, Beneras, and Bangalore.

#### The Problem Situation

The Ace Tomato Company needs a secure remote-access solution for its external end-users.

#### Business Requirements

The business requirements provided by the Ace Tomato Company are as follows:

- Must support strong level on encryption (Triple-DES or above)
- Must be accessible from all types of networks, including NAT’d networks, remote offices, hotel rooms, behind internal proxy servers, and organizations that allow only TCP port 80 and 443 outbound
- Must support two-factor authentication
- Must be able to provide easy access to e-mail and intranet servers from internal networks, DMZ networks, and extranets
- Must be able to provide secure file-sharing access
- Must require only a single action from novice end-users for e-mail
- Must provide stable and consistent performance

Secure remote access is one of the premier reasons to use SSH, especially with its port-forwarding feature. Despite the fact that port forwarding will be used, the type of SSH solution chosen for this particular architecture is very important, since not all SSH solutions can meet all of the preceding requirements with the same level of simplicity.

For your solution, you will choose to use the Vshell SSH server due to its ability to provide secure file-sharing access without the need for additional file-system restrictions, such as NTFS or Unix file-system security. Since remote access to e-mail, file sharing, and intranet Web pages are the only requirements, VShell also provides the ability to easily restrict command-line access to the SSH server, a feature that must be enabled for all users to secure the SSH server itself. Furthermore, since your remote-access solution requires access behind internal proxy servers, SecureCRT is a great solution, since it can connect through proxy servers using a CONNECT string, as discussed in Chapter 9. Lastly, SecureCRT also offers the ability to automatically execute other applications, such as e-mail clients, once an SSH connection has been established. This will meet the requirement that states that all novice users should have only one step to access e-mail.

In addition to SecureCRT, SSH Communications’ SFTP client will be used to access the SFTP session on the Windows file server, since SecureCRT does not have a built-in SFTP client. This will require an additional step for file-sharing access; however, that does not break any of the preceding requirements. The following list states the utilities that will be used:

- VShell for the SSH servers
- SecureCRT for the SSH client
- SSH Communications for the SFTP client

The key requirements from an architecture perspective will be the ability to access e-mail servers, file sharing, and intranet Web servers from the SSH server. Also, since command-line access to the SSH server is not desired, command-line access will need to be restricted. Furthermore, since the internal file server will need to be accessible remotely, another installation of VShell should be installed on the internal file server for remote SFTP users. Figure 10.1 shows the remote-access architecture.
