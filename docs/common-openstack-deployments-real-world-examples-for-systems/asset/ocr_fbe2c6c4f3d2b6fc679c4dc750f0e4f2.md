your chosen base operating system or provide access to port 80 to that machine from another machine. This is so you can use the web browser on localhost or install the server version with a bridged interface so the server is accessible from the outside. If you're using physical hardware, make sure the system is accessible via the network.

# ## Deploying DevStack

Now that you have the required resources to run DevStack, you have some configuration decisions to make.

DevStack is designed to be run out of the box, with no configuration changes, with a series of simple commands, the last of which will take some time:

```
```
$ sudo apt-get install git
$ git clone https://git.openstack.org/openstack-dev/devstack.git
$ cd devstack
$ . /stack.sh
```
```

The first few steps will ask you for a series of passwords for each component. You will want to take note of what you put in for these passwords. Once it has the passwords, it will take some time as it modifies your software sources and networks and then downloads requirements and the latest development version of OpenStack components used in DevStack. The script will also pause at some points in the beginning to ask you for service passwords (see the section “Customizing DevStack” later in this chapter for tips on how to use a local.conf file with these variables instead).

The DevStack project provides a commented version of the stack.sh script for perusal while the default install takes place; you can view it locally in the devstack directory or online at http://docs.openstack.org/developer/devstack/stack.sh.html.

# Common Failures

If your permissions are not correct, you will have problems running DevStack. Here are a few tips:

+   - Do not use root or sudo when running any of the commands outlined above.
+   - While you shouldn’t run the commands as root or sudo, the user you’re running stack.sh with must have sudo access, preferably passwordless.
+   - When you are running stack.sh, confirm the devstack/ directory is owned by the user you are attempting to run it with.
+   - If you wish to create a “stack” user specifically designed for running DevStack, you can use the tools/create-stack-user.sh script that ships with DevStack. This script needs to be run with sudo from an account with sudo access.

Networking is the root cause of many failures. The following are some of the most common problems:

+   - Your local network conflicts with the default setup of DevStack’s internal network (10.0.0.1/24).
+   - The VM or physical system cannot access the Internet. Internet access is required to run stack.sh. This can manifest as anything from name resolution errors to timeouts to the operating system repositories.