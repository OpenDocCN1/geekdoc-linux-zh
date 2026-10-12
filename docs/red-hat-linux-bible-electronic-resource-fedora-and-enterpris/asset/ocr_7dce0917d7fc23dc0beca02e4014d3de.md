You can also set your computer to broadcast to the local network for your NIS server. If your domain were named trident, for example, you would use the domain/broadcast option as follows:

```
domain trident broadcast
```

If the address of your NIS server is contained in your /etc/hosts file, you can specify that ypbind look in that file to find the server's IP address. For example, if your NIS master server is named maple, you would add the following entry:

```
ypserver maple
```

When ypbind starts, all the information in this file is read. It is then used to contact the appropriate NIS server.

# ## Configuring NIS client daemons

After your NIS client information is all set up, all you need to do to run NIS as a client is start the ypbind and ypwhich daemons. The ypbind daemon runs continuously as two processes: The master ypbind process handles requests for information from your NIS server, and the slave ypbind process checks the bindings from time to time. The ypwhich daemon finds your NIS master server.

Getting these daemons running is pretty easy. You can set up an existing run-level script called ypbind to start automatically at boot time. To do this, you can run the following command (as root user from a Terminal window):

```
# chkconfig ypbind on
```

To start the ypbind daemon immediately, type:

```
# /etc/init.d/ypbind start
```

> CROSS-REFERENCE: For more information on run-level scripts, refer to Chapter 12.

# ## Checking that NIS is working

To check that your NIS client is communicating with your NIS master server, follow the instructions in this section.

> NOTE: If your NIS server isn't configured yet, refer to the "Setting Up Red Hat Linux as an NIS Master Server" section later in this chapter to configure your NIS server. Then return to this procedure to make sure that everything is working properly.

From the NIS client computer, type the following command to make sure that you are communicating with the NIS server:

```
# ypwhich
maple
```