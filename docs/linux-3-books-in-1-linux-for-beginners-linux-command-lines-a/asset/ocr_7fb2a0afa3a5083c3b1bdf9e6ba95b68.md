*serviceName off.*

# ## Disabling Login through the Root

As mentioned earlier, it is important to ensure that you do not log in to your server using the root account. Therefore, you need to disable the ssh port as the root account on the server's configuration file. Before you do this, let us look at an example where we create a user with sudo privileges, so you can use the ssh port to access the server and perform the necessary tasks. When you log in to the server, you can move from the user to the root account if you need to. Let us first create a new user. To do this, use the following command: `useradd user1`. You can now add a password to this user account using the command: `passwd user1`. Now that you have a user created on the server, you can give it sudo permissions using the following line: `echo 'user1 ALL=(ALL) ALL' >> /etc/sudoers`. You then need to use ssh to access the server using the new user account. This is one way to ensure you log in to the server.

Now, we need to disable the root access to the SSH port. This will mean no user can use SSH to log in to the server using the root account. You need to open the configuration file `nano /etc/ssh/sshd_conf` to do this. You then need to update the line `PermitRootLogin` to no in the file. You then need to save this file and close it. Once you restart it, you will see that the settings have been updated.

Before you log out of the server, you should test if you can log in to the server using SSH using a user ID that was created earlier. To do this, you can open another instance in the terminal and log in to the council using SSH. If everything works as it should, you can log out of the server as the root user.

# ## Change Ports

You can also change the default port used by SSH to access the network. You can add a layer of security to ensure your server is safe. To do this, you need to make updates to the `/etc/ssh/sshd_config` file. In this file, you need to replace port number 22 with a number you want to use as the port. Once you save the file down, you can reboot the server. To do this, you need to use the following command: `service sshd restart`. You can then log in to the server using the updated port number with the following command: `ssh`