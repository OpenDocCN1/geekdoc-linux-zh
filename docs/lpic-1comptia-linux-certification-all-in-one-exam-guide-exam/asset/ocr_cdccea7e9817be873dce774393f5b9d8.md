Now that you understand how SSH connections are established, you need to learn how to configure OpenSSH.

# Configuring OpenSSH

To use ssh, you must first install the openssh package on your system from your distribution media. This package includes both the sshd daemon and the ssh client. OpenSSH is usually installed by default on most Linux distributions. You can use the package management utility of your choice to verify that it has been installed on your system.

The process of configuring OpenSSH involves configuring both the SSH server and the SSH client. You configure the sshd daemon using the /etc/ssh/sshd_config file. The ssh client, on the other hand, is configured using the /etc/ssh/config file or the ~/.ssh/ssh_config file.

Let's look at configuring the SSH server (sshd) first. There are many directives within the /etc/ssh/sshd_config file. The good news is that after installing the openssh package the default parameters work very well in most circumstances. To get sshd up and running, you shouldn't have to make many changes to the sshd_config file. Some of the more useful parameters in this file include those shown in Table 18-1.

| Option | Description |
| :--- | :--- |
| AllowUsers | Restricts logins to the SSH server to only the users listed. Specify a list of users separated by spaces. |
| DenyUsers | Prevents the users listed from logging in through the SSH server. Specify a list of users separated by spaces. |
| HostKey | Specifies which private host key file should be used by SSH. As discussed previously, the default private key file for SSH version 1 is /etc/ssh/ssh_host_key for protocol version 1 while SSH version 2 can use the /etc/ssh/ssh_host_rsa_key and /etc/ssh/ssh_host_dsa_key files. You can configure sshd to use multiple host key files. Be aware that if a key file has read or write permissions assigned to group or others, sshd will refuse to use it. |
| ListenAddress | If the host where sshd is running has multiple IP addresses assigned, you can restrict sshd to only listening on specific addresses using this parameter. The syntax is ListenAddress IP_address:port. |
| PermitRootLogin | Specifies whether you can authenticate through the SSH server as root. |
| Port | Specifies the port on which the sshd daemon will listen for SSH requests. |
| Protocol | Specifies which version of SSH to use. Specify one of the following:
  * 1 Configures SSH version 1.
  * 2 Configures SSH version 2.
  * 2,1 Configures sshd to support both SSH versions, but preference is given to version 2. |

Table 18-1 Options in the sshd_config File