In this chapter, we are going to cover the following main topics:

+   - A complete guide to Unix services (how they work and how to manage them)
- Permissions work on Unix systems
- A detailed overview of the different types of permissions on Unix systems (file, folder, user, and so on)
- Advanced configuration of permissions using umask
- Enhancing your defensive security by using access controls
- Managing access control lists
- Configuring your host-based firewall using iptables
- Best practices to leverage log files

# Technical requirements

For this chapter, it is highly recommended that you have a Unix-like system (this could be Kali Linux, Debian, Ubuntu, and so on). This chapter contains a lot of screenshots that you can see the output of the commands used. However, it will be of great value if you can test these commands yourself while enjoying the book.

A very good option is to create a Virtual Machine (VM) so you can run it through Kali easily on your computer. In fact, you will find at the end of this chapter the link to the Kali Linux download page. There you can download a preconfigured VM, ready to open in your favorite hypervisor (VirtualBox, VMware, and so on).

# Securing Unix services

Services are applications that run in the background to perform or support essential Operating System (OS) tasks. There are also services associated with apps or services such as Apache, Structured Query Language (SQL), Hypertext Preprocessor (PHP), Remote Procedure Call (RPC), and so on.

A lot of services are loaded and enabled by default. However, every service enabled and running presents a potential vulnerability that needs to be considered and managed.