![](bbox=[0.14, 0.08, 0.81, 0.26])

# Figure 4.7 Key-based authentication in SSH.

Furthermore, I will demonstrate how to convert specific SSH client keys to fit a particular SSH server. For example, OpenSSH keys are not interpretable to SSH Communications’ SSH servers by default. While it would be very nice if all public and private keys could be used from one SSH server to the other, the reality is that you need to modify your public and private keys in order to use them across multiple environments. The SSH servers you will make your client keys interoperable with are the following:

+   * SSH Communications
+   * OpenSSH
+   * VShell

> **NOTE** In the following sections, the use of ssh, ssh-keygen, ssh.exe, and ssh-keygen.exe refers to OpenSSH SSH clients. Further more, the use of ssh2, ssh-keygen2, ssh2.exe, and ssh-keygen2.exe refers to SSH Communications’ SSH clients. Lastly, the use of vsh.exe and vcp.exe refers to VanDyke Software SSH clients.

# ## Creating Keys with OpenSSH

To create keys with the OpenSSH client, complete the following steps on the client machine.

+   1. Change directories to the location of the ssh-keygen binary:
+   ``` cd /usr/bin C:\cd *Program Files*\OpenSSH\bin ```

+   2. Create a DSA key pair:
+   ``` #ssh-keygen -d C:\Program Files\OpenSSH\ssh-keygen.exe -d Generating public/private dsa key pair. ```