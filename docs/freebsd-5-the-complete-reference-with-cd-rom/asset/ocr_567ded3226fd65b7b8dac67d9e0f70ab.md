# # Methods of Starting Servers

One of the most fundamental aspects of server configuration is running the server. This goal can be accomplished in three different ways: You can run the server manually, you can run it automatically in a startup script, or you can use an intermediary server to monitor the target server’s port and launch the target server only when its services are needed. Each approach has its unique advantages and disadvantages, not to mention its own configuration files. Thus, understanding these methods is important to administering network servers.

# ## Manually Launching Servers

When you first configure a server, you may want to launch it manually. This process works just like launching any other program: You type the program’s name at a command prompt, possibly along with some options. For instance, you can use the following command to launch the smbd server (part of the Samba package, described in Chapter 18):

```
# smbd
```

Many servers automatically detach themselves from your shell when launched in this way, so your shell prompt will return immediately. Others remain attached to your shell, so they can display error messages for debugging purposes. If you want to leave such a program running for an extended period of time, you can follow its name with an ampersand (&) to have it detach from your shell.

The drawback to launching a server manually is that it’s a one-time affair. If a computer should always run half a dozen servers, it’s inconvenient to have to launch them manually whenever you reboot the computer. Indeed, if the computer reboots automatically (say, because of a power failure), you may not be able to launch the server for some time. Thus, some automatic methods of launching servers exist.

# ## Using Direct Startup Scripts

Chapter 6 describes FreeBSD’s main startup scripts. These scripts control programs that FreeBSD runs whenever it starts. Thus, one way to configure a server to run automatically is to add a reference to the server in a startup script. The two main classes of scripts in which such references may appear are

+   * /etc/rc.\* scripts. These scripts control the standard startup process. The /etc/rc.d/network script is particularly important because it includes routines to start many common network servers. The /etc/rc.conf file includes configuration options to enable or disable specific servers. For instance, including sshd_enable="YES" in this file enables the Secure Shell (SSH) server (described in Chapter 21).