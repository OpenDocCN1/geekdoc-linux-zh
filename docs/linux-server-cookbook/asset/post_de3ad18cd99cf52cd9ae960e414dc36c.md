
## Conclusion

Networking is one of the core parts of the Linux server. Modern services rely on networking, and knowledge about advanced features is required when virtualization and containers are involved. This chapter covered topics from the basic concept of the network to the most advanced ones, such as bridging and virtual LANs.

## Key facts

- OSI model knowledge is required to understand traffic flow.
- Linux provides several tools to check connectivity.
- Network configuration is configured using Network Manager or netplan.
- Linux eases advanced network configuration with simple tools.

## Questions

- How many layers are part of the OSI Model?
    - Five layers
    - Seven layers
    - Nine layers
- In which layer the routing is placed in?
    - First layer
    - Second layer
    - Third layer
- What is the default tool to configure networking on a Ubuntu server?
    - netplan
    - NetworkManager
    - systemd
- Which command on NetworkManager is used for the text user interface?
    - nmtui
    - nmcli
    - nmui
- What key is required to be enabled for IP forwarding?
    - net.ipv4.forwarding
    - net.ipv4.ip_forwarding
    - net.ipv4.ip_forward
- What directory contains files with the bonding information?
    - /sys/net/bonding/
    - /proc/net/bonding/
    - /dev/net/bonding/

## Answers

1. b
2. c
3. a
4. a
5. c
6. b

## CHAPTER 8: Security

## Introduction

Offering a service to end users leads to possible security risks, such as data leaks or unauthorized access. Though Linux is the most secure operating system, it is necessary to avoid unwanted access to the service or to the system itself. To protect a system, there are two main important points: keep the system updated to avoid attacks on the software in the system, and protect who has access to the system through the network.

This chapter is focused on network security using a firewall and limiting access to different services using configuration. Linux also provides different tools to avoid the execution of unwanted software and checks if the system is compromised.

## Structure

In this chapter, we will discuss the following topics:

- Security introduction
- Firewall configuration on Linux
- Services security
- Network monitoring

## Security introduction

One of the main tasks of Linux system administrators is to keep the system updated and protected from unwanted access to the system itself or applications. [Chapter 4, User Administration and Software Management] describes how to create users and groups and how, by using permissions, it is possible to limit access to files and directories. It is important to protect the system by checking the files using special permissions, to avoid unwanted permission escalation. The process of protecting a system from a default installation is called *hardening*.

Security networking uses this knowledge to protect the system from remote access, either from a user or system in the same network or an attacker from outside of the network through the internet. The main security related to networking is to use a Firewall on the Linux system. Even though the network would be protected by a network firewall, it is important to protect the systems with their own firewall to create double protection.

Historically, firewall configuration in Linux was a complicated task that required knowledge about *iptables*, a tool to maintain filter rules in the Linux kernel. Modern distributions include high-level tools to manage firewall rules, helping administrators and regular users to manage firewall rules in an easy way.

Depending on the Linux distribution used, the default firewall tool will be different. Red Hat Enterprise Linux and derivatives, such as CentOS Stream or Rocky Linux, rely on the *Firewalld* project as firewall management. Ubuntu distribution uses an *Uncomplicated Firewall (ufw)* as the default configuration tool to ease firewall configuration.

The default backend for the firewall solutions in modern distributions is *nftables*, which replaces the traditional *iptables*. It is possible to use the command *nft* to manage or list the rules configured in the system.

![](img/863afa537de4eed7deb11978bfbfa90e_244_0.png)

*Figure 8.1 shows packet flows through Linux networking*

Linux services implement their own security configuration. For example, the service *SSH* allows to configure to not allow login with the administrator user *root* or only allows the connection using *SSH public/private keys*. Another example is NFS Server, which limits the exported directories to specific IPs/Network ranges and with the possibility to enable authentication.

Another protection solution offered by the Linux distributions is called *mandatory access control* policies. This security is a proactive approach that helps to protect the system against both known and unknown vulnerabilities. These policies enforce what the application and the user can do, such as access to directories, the ports they can use, or the operations they can do. For example, it protects a Web server to access a directory that is not the default or denies the connection from the Web server to a remote location.

Red Hat Enterprise Linux and derivatives offer **Security-Enhanced Linux (SELinux)** for supporting **Access Control Security Policies**. Debian and Ubuntu rely on *AppArmor* solution as **Mandatory Access Control (MAC)**.

Other security-related management examples on Linux for *hardening* include the following:

- Disk encryption: Using **Linux Unified Key Setup (LUKS)** for hard drive encryption.
- Secure user access: Includes **Pluggable Authentication Modules (PAM)** configuration, the configuration of user *limits*, the configuration of *sudo*, and user auditing, among others.
- Restrict file-system permissions: It is possible to restrict which directories can contain executables and what directories should be read-only.

Linux distributions offer the possibility to comply with three popular security certifications, which usually are required for companies in the public sector or companies working with sensible data:

- **Federal Information Processing Standards Publications (FIPS)**: Issued by the **National Institute of Standards and Technology (NIST)**, the *FIPS 140-2* specifies the security requirements for cryptographic modules.
- **Center for Internet Security (CIS)**: It publishes benchmarks related to services. They offer **Extensible Configuration Checklist Description Format (XCCDF)** format benchmarks, which can be used by different tools.
- **Security Technical Implementation Guides (STIG)**: Developed by the **Information System Agency (DISA)** for the **US Department of Defense (DoD)**, STIG consists of security controls, including configuration settings to hardening Linux distributions.

## Firewall configuration on Linux

One of the common tasks performed during the installation is to configure the Firewall. The considerations to have a secured firewall configuration are as follows:

- Block by default; if there is not a specific rule, then the connection should be rejected.
- Open only the ports needed for the services and specify the protocol for those ports.
- Limit the connection from specific IPv4 or IPv6 addresses.
- Apply the rules to specific network interfaces in the system.
- Limit the rate of the connections to avoid attacks.
- Automate firewall rules with an automation solution (for example, Ansible).

## Firewalld

Firewalld provides a dynamically managed firewall with zones that define the trust level of network connections or interfaces. A big benefit of the usage of firewalld, is the possibility to perform changes in the rules without having to restart the service. It uses **Desktop Bus (D-Bus)** as a message bus system, a simple way for applications to talk to each other. Firewalld has different support for several backends. *Figure 8.2* illustrates the structure:
