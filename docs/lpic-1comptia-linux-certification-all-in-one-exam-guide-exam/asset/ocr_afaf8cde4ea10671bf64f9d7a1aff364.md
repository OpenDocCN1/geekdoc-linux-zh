The whole reason this process works is because only the private key can decrypt a message encoded by the public key. For example, a hacker could easily intercept the public key used in the transaction in Figure 18-3. But that's not a problem because it can't be used to decrypt information encrypted with the same public key (in this case, the credit card submission). That can only be done by the private key, which is kept safe on the web server and is never transmitted openly.

Because your Linux system installed its own CA when you initially installed the system, you can use it to mint your own certificates and use them to encrypt both network transmissions and files in the file system. Let's review how this is done next.

# # Encrypting Remote Access with OpenSSH

In the early days of UNIX/Linux, we used a variety of tools to establish network connections between systems. You could access the shell prompt of a remote system using Telnet, login, or rsh. You could copy files back and forth between systems using rcp and FTP. However, these utilities had one glaring weakness. Network services such as Telnet, login, rcp, rsh, and FTP transmit data as clear text. Anyone running a sniffer could easily capture usernames and passwords along with the contents of the transmissions.

For example, suppose I remotely accessed my Linux system via Telnet. After authenticating to the remote system, I decided that I needed to switch to root using the su command to complete several tasks. If someone were sniffing the network wire while I was doing this, they would be able to easily grab the following information:

+   - My username and password
+   - The root user password

This is not a good thing! The attacker now has everything he needs to gain un- fetered access to my Linux system.

To prevent this from happening, you can use the OpenSSH package to accomplish these same management tasks using encryption. In this part of the chapter, you will learn how to use OpenSSH. The following topics are addressed:

+   - How OpenSSH works
+   - Configuring OpenSSH
+   - Tunneling traffic through SSH
+   - Configuring SSH to use public key authentication

Let's begin by discussing how OpenSSH works.

# ## How OpenSSH Works

OpenSSH provides the functionality of Telnet, login, rsh, rcp, and FTP, but it does so using encryption. To do this, OpenSSH provides the following encryption-enabled components:

+   - sshd This is the ssh daemon that allows remote access to the shell prompt.