+   * **Appendix E: OpenStack Client (OSC)**   The OpenStack Client is rapidly replacing individually maintained clients for each project. This appendix provides some background and a quick reference for some common commands.
+   * **Appendix F: Finding Help with OpenStack**   The final appendix provides a quick tour of the support options in the OpenStack community, both online and in person. It concludes with tips for finding paid support as well.

# ## Conventions

Instead of using the root user, sudo is used throughout this book. As such, all commands are prefixed with a dollar sign to indicate that it's a command you should be typing into a shell. For instance, when you're preparing your Ubuntu systems and want to update the Ubuntu sources before installing anything, we show that as:

```
$ sudo apt-get update
```

When lines are wrapping, we use the bash syntax of `\` to indicate that the command wraps to the next line. The creation of a compute instance is a good example of this:

```
$ openstack server create --flavor m1.tiny --image "Cirros 0.3.4" \
--security-group default --nic net-id=network1 \
--availability-zone nova my.first_instance
```

For most of the OpenStack commands, we have provided sample output of what to expect when you run each command. For the output of standard tooling for things like Ubuntu package installation, git clones and MySQL commands, this output is generally not included.

# ## Supplementary Materials

As discussed, you will need a copy of the Ubuntu 14.04 ISO to install Ubuntu on your initial OpenStack controller and compute nodes. Later, the Ubuntu 14.04 server QCOW2 cloud image will need to be loaded into Glance for our deployment example using Ubuntu as a compute instance. All Puppet modules and other packages are downloaded through scripts you're instructed to use or through Puppet itself.

This book also has an accompanying git project hosted on GitHub at https://github.com/DeploymentsBook.

This project is broken into several repositories:

+   * **http-files**—Used for our basic web server examples.
+   * **puppet-data**—The repository you clone to bootstrap your installation of Puppet on your OpenStack nodes. It also includes your core configuration file, hiera/common.yaml, which you will be editing.