
The .log files inside each VM’s directory maintain a log of all of the events that happen to a VM. You can access a subset of these logs from within the Web interface, but the log files themselves contain much more detailed information. Look here if a VM crashed for some unexpected reason or if you just want a lower-level understanding of what VMware does when you start or stop a VM.

Since everything that makes up a VM is really just a file on the system, provided that a VM is suspended or powered off, you can move the files around with regular Linux commands like mv, cp, and rsync. If you want to migrate or copy a VM from one machine to another, you could just make sure it is powered off or suspended and then use rsync or scp to transfer it. Keep in mind that when you do move or copy a VM and start it back up on a new host, VMware will detect it and prompt you to generate a new UUID (a universal string that should be unique for each VM).

## Virtual Appliances

Another useful aspect of all VM settings and disks residing in one directory is that a number of people have created what are known as “virtual appliances.” Essentially a virtual appliance is a VM created for a particular purpose such as a spam filtering or a firewall. A number of companies have even set up virtual appliances that have their software pre-installed so you can easily demo it. Virtual appliances are generally compressed into a single .zip file, so once you download them, all you have to do to install them is extract the .zip file into /var/lib/vmware/Virtual Machines, go to the Web interface, click Virtual Machine_Add Virtual Machine to Inventory, and then browse to the new VM’s .vmx file. VMware itself hosts a number of virtual appliances on its site and even has a link on the Web interface called Virtual Appliance Marketplace that will take you right there.

## Ubuntu Enterprise Cloud

If you have been following the virtualization world at all, you no doubt have heard the term cloud, probably used in reference to Amazon’s Elastic Computing Cloud (EC2) service. Amazon has built a large infrastructure of servers that can run VMs. Amazon then sells time and resources on these machines so that you can deploy your own virtual servers on Amazon’s infrastructure and no longer have to worry about storage, RAM, or CPU resources or even what physical server your VM runs on. Instead the server runs somewhere on Amazon’s cloud.

While it is straightforward and simple to deploy your own Ubuntu servers on EC2, some administrators prefer having full control over their infrastructure, both physical and virtual. Ubuntu has provided a solution called Ubuntu Enterprise Cloud (UEC) that allows you to set up your own “private cloud”—a set of your own servers that can run VMs and behaves much like EC2. With UEC you can add multiple nodes to your own cloud and manage it and all of your VMs from an easy-to-use interface.

While you might expect it to be rather difficult to deploy your own private cloud, Ubuntu has greatly automated the process, and as you’ll find, it only takes a couple of steps. First though, let’s go over what you will need.

## UEC System Requirements

At a minimum you will need two physical servers to run UEC, a front-end server and one node. The front-end server will manage your private cloud and provide the following services:

- The Cloud Controller (known as cic)
- The Cluster Controller (known as cc)
- Walrus (the storage service like Amazon’s S3)
- The Storage Controller (known as sc)

Since the front-end server itself will not run any VMs, you can use an older server that doesn’t support virtualization extensions. The front-end server will also store all of the different server image types and deploy them to each node over the network so the more (and faster) storage and network speed you have for this machine, the better.

The node server is one of potentially many servers that are managed by the front end and will actually run the VMs themselves with the node controller (nc) service. Your node servers will need support for virtualization
