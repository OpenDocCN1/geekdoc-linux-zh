to the **/etc/yppasswd** file using standard tools such as **useradd** and **userdel**, or their graphical counterparts, and then running **ypinit** (page 784) to update the map.

# # SETTING UP AN NIS SERVER

This section explains how to install and configure an NIS server.

# ## PREREQUISITES

Decide on an NIS domain name (page 774) and install the following packages:

+   *   **ypserv**
+   *   **rpcbind** (installed by default)

**Check **rpcbind** is running**  A new Fedora/RHEL system boots with **rpcbind** installed and running. Use the **systemctl status** command to make sure the service is running.

```
# systemctl status rpcbind.service
```

After modifying **rpcbind** configuration files, give the second command again, replacing **status** with **restart** to cause **rpcbind** to reread those files.

**Enable and start **ypserv**** Run **systemctl** to cause the **ypserv** service to start each time the system enters multiuser mode and then start the **ypserv** service. Use the **systemctl status** command to make sure the service is running.

```
# systemctl enable ypserv.service
# systemctl start ypserv.service
```

After modifying **ypserv** configuration files, give the second command again, replacing **start** with **restart** to cause **ypserv** to reread those files.

**Enable and start **ypxfrd**** The **ypxfrd** map server service speeds up the process of copying large NIS databases from the master server to slaves. It allows slaves to copy the maps, thereby avoiding the need for each slave to copy the raw data and then compile the maps. When an NIS slave receives a message from the server saying there is a new map, it starts **ypxfrd**, which reads the map from the server.

On the master server only, run **systemctl** to cause the **ypxfrd** service to start each time the system enters multiuser mode and then start the **ypxfrd** service. Use the **systemctl status** command to make sure the service is running.

```
# systemctl enable ypxfrd.service
# systemctl start ypxfrd.service
```

After modifying **ypxfrd** configuration files, give the second command again, replacing **start** with **restart** to cause **ypxfrd** to reread those files.

**Enable and start **ypasswdd**** In addition, on the master server only, run **systemctl** to cause the NIS password update service, **ypasswdd** (page 785), to start each time the system enters multiuser mode and then start the **ypasswdd** service. This service will not start if the NIS domain