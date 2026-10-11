
server.

```bash
$ sudo firewall-cmd --add-service http --permanent
$ sudo firewall-cmd --reload
```

You should test this inclusion using an external browser:

```bash
$ curl --silent 192.168.122.206 | grep title
<title>Test Page for the Apache HTTP Server on Red Hat Enterprise Linux</title>
```

Now, you know how you can include or add a service to your web server. It is, therefore, easy for you to remove one.

```bash
$ sudo firewall-cmd --remove-service http --permanent
$ sudo firewall-cmd --reload
```

## Removing and Adding Ports

You may have trouble with finding a predefined service on your system or network. The network or the ports may also assume that the defaults used do not match, and they may reject the access. Instead of adding a service to your firewall, you can add a protocol type or port number using the command `--add-port`. For example, if you want to use a non-standard port for the SSH protocol in your custom zone, you can add the details using the commands below:

```bash
$ sudo firewall-cmd --add-port 1622/tcp --permanent
success
$ sudo firewall-cmd --reload
```

To remove that port, use `--remove-port`:

```bash
$ sudo firewall-cmd --remove-port 1622/tcp --permanent
success
$ sudo firewall-cmd --reload
```

## Walls of Fire

You can do quite a bit using the firewall-cmd command, which is not listed above. You can define ICMP blocking, define the sources which can send data and traffic to your system using the network, or even define the services you want to permit. It is easy for you to learn by experimenting. So, you can install Fedora or Red Hat Enterprise Linux in a GNOME box. This will allow you to play around with traffic and shape it using the firewall-cmd command's different options.

## Chapter Four

### Securing Your Server

In the previous chapter, we looked at how you can secure the server using a firewall. We also looked at the importance of user accounts and other details. In this chapter, we will look at the different ways to secure a server without using a firewall.

### Updating Servers Regularly

If you can access the server as the administrator, you need to update it regularly. To do this, run the following command: `apt-get update && apt-get upgrade`. It is important to ensure while you run the upgrade that you are on a VPS or virtual instance. This can damage the image and the server. So, you need to check if you can do this on your host.

### Creating a Secondary User Account

You need to do this to ensure no user logs into the server using the root account. If you want to reduce the probability of unauthorized access on your server, you need to create a user and ensure you give them the relevant privileges to ensure they cannot perform unauthorized activities on the server. We have looked at how you can add new users to the servers. If you want the user to have access to the server with a specified set of privileges, you can give him sudo access.

You need to update these terms in the configuration file. Once you do this, you can save and close the file down. You need to ensure the user can access the server the way he needs to, and you can confirm this by logging into a second terminal on the same server. It is especially important for you to do this. Let us now remove the root users who access the server through SSH. If you want to accomplish this, you need to edit the configuration file: `/etc/ssh/sshd_config`. It is important to ensure you are logged into the same server using a different shell before you reload the SSH. This is to ensure you do not log yourself out of the server. Now, open the configuration file and update the line `#PermitRootLogin yes` to `PermitRootLogin no`. You can then restart the service using the following command:

```bash
/etc/init.d/sshd restart
Stopping sshd: [ OK ]
Starting sshd: [ OK ]
```

Bear in mind that Linux does not have a default root password when you install the operating system on your server. There is no root login, but you, as an administrator, will have sudo privileges and administrative access.

### Setting up SSH Keys

An SSH key on your server allows you to connect securely to the server using an authorized key pair. This is an extra step you need to perform to ensure the server is secure from any unauthorized access. You need to log in to SSH using the root user account and run the following command: `ssh-keygen -t rsa -C "you@example.com"`. Once you click on accept, the default file locations and names will be added to the server along with the file names. You can re-enter the password for your user account and add the public key to the file on your server. Use the following lines of codes to do this:

```bash
cd ~/.ssh
cp id_rsa.pub authorized_keys
```

You should now copy the public key to the SSH directory in the root account that is present on the server. To do this, you can run the following commands:

```bash
cd ~/.ssh
scp authorized_keys root@host.servername.com:/root/.ssh/
```

You can now connect with the server directly.

### Checking and Configuring the Firewall

Run the following commands to check and configure your firewall. You can also do it using the information present in the previous chapter.

```bash
root@server:~# ufw app list

Available applications:
OpenSSH
```

```bash
root@server:~# ufw status
Status: active
To                          Action      From
--                          -------     ----
22/tcp                      ALLOW       Anywhere
22                          ALLOW       Anywhere
8080/tcp                    ALLOW       Anywhere
80/tcp                      ALLOW       Anywhere
Anywhere                    DENY        58.218.92.34
80                          DENY        202.54.1.5
22 (v6)                     ALLOW       Anywhere (v6)
22/tcp (v6)                 ALLOW       Anywhere (v6)
8080/tcp (v6)               ALLOW       Anywhere (v6)
80/tcp (v6)                 ALLOW       Anywhere (v6)
```

### Limiting the Use of Open Ports

When you install Linux on your system, you do not have to worry about any network services listening to and monitoring the data you are passing through the server. When you start the server, you can determine who the administrator and root users should be and determine the various ports and services that can use the server. You need to test the open ports on your server. To do this, run the following lines of code:

```bash
root@server:~# /home# netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State PID/Program name
tcp     0      0 0.0.0.0:22                0.0.0.0:*               LISTEN 69941/sshd
tcp6    0      0 :::22                     :::*                    LISTEN 69941/ss
```

### Setting Up Live Kernel Patches

You can use the canonical livepatch service to determine when your server needs a security fix, especially when it comes to major kernel securities which do not reboot. As a Linux user, you can take advantage of these services for free up to three zones or nodes. Every machine that is a part of the subscription can find a way to fix security issues and vulnerabilities. You can learn more about these tools on the Linux website.

### Hardening the Kernel

There are different built-in protections in a kernel, and you can use these methods to ensure the kernel is not compromised.

### Hardening User Space

You need to learn more about how you can harden the user spaces. You can use different hardening tools and applications to do this. A common option is to use a compiler flag when you build a tool or application. This is especially true if you use the kernel to launch the application. You can add additional features to the application or tool if you need to. It is important to remember that these additional features can be added to all applications on the server, not just the operating system's official apps.

### Using Secure Boot

When Linux developers launched Ubuntu, they included a secure boot to the operating system. The developers added the secure boot option, enforced it in the bootloader, and switched on the kernel's non-enforcing mode. With this setup, the versions that could not authenticate secure boot failed to boot, and the kernels did not validate the authentication, either.

### Setting Up Two-Factor Authentication

If you want to add an additional protection layer to your server, you can set up multi-factor or two-factor authentication on the server. You need to be careful about setting this up, because you can lock yourself if you incorrectly enter the password. To do this, follow the steps below:

- **Step One**
  - Access the server through SSH and run the following command to use Google as your authentication mechanism.
  
  ```bash
  apt-get install libpam-google-authenticator
  ```

- **Step Two**
  - You should now run the command google-authenticator to create a secret key in your server's home directory.
  
  ```bash
  google-authenticator
  ```
  
  *Do you want authentication tokens to be time-based (y/n)* y
  
  *Your new secret key is: 73GRSXVJNUXZWN2T*
  
  *Your verification code is 389485*
  
  *Your emergency scratch codes are:*
