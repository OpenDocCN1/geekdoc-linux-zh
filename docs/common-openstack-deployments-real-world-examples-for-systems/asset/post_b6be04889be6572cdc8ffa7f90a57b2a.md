
In the `[oslo_messaging_rabbit]` section you'll want to update it to point to your controller's address and inform it of the Rabbit user and password:

```
rabbit_host = controller
rabbit_userid = openstack
rabbit_password = RABBIT_PASSWORD
```

Next, edit `/etc/neutron/plugins/ml2/openvswitch_agent.ini` and add the following to the `[agent]` section:

```
tunnel_types = vxlan
```

In the `[ovs]` section, update the `local_ip` to be its own IP and enable tunneling:

```
local_ip = 192.168.122.5
enable_tunneling = true
```

The final change to make to this file will be to specify the iptables firewall driver to use for the security groups:

```
firewall_driver = neutron.agent.linux.iptables_firewall.OVSHybridIptablesFirewallDriver
```

Next you'll want to edit your `/etc/nova/nova.conf` file to add the `[neutron]` section to your configuration:

```
[neutron]
auth_url = http://controller:5357/v3
url = http://controller:9696
auth_plugin = v3password
project_domain_name = default
user_domain_name = default
project_name = service
username = neutron
password = NEUTRON_PASSWORD
ovs_bridge = br-int
region_name = RegionOne
timeout = 30
extension_sync_interval = 600
```

Restart the Neutron OVS agent and the compute services to apply your changes.

```
$ sudo service nova-compute restart
$ sudo service neutron-openvswitch-agent restart
```

## Manage an Instance

Congratulations, your system is now running a bare bones OpenStack configuration with Keystone, Glance, Nova and Neutron, which you can interact with through the command line. We've completed small tests for each component to confirm they are working, and now it's time to test that everything has come together to create instances on your new OpenStack installation. Up until now we've been using an `openrc.admin` file to load up the administrative credentials for your cloud, but now you'll want to create a testrc file that uses the test user we configured earlier. The test user cannot run some commands that the admin user can, such as `openstack user list` or `openstack endpoint list`, but is the appropriate account to use as we start launching instances and using OpenStack as a user. With that in mind, we'll load up the test user environment variables:

```
$ source ./topcmerc.test
```

Now you will want to adjust the default security group for *test user* so that you can use SSH and ping in your new instances.

```
$ openstack security group rule create --proto tcp \
--src-ip 0.0.0.0/0 --dst-port 22 default
```

| Field | Value |
| :--- | :--- |
| id | 9ed83108-dbc4-45fd-beaf-e1c1dd7f1c14 |
| ip_protocol | tcp |
| ip_range | 0.0.0.0/0 |
| parent_group_id | a861046e-9cba-4f1a-ab2c-833d7e27c122 |
| port_range | 22:22 |
| remote_security_group | |

```
$ openstack security group rule create --proto icmp \
--src-ip 0.0.0.0/0 --dst-port -1 default
```

| Field | Value |
| :--- | :--- |
| id | 6acfea29-5ada-4ead-d48f-8f2a13cf1aa7 |
| ip_protocol | icmp |
| ip_range | 0.0.0.0/0 |
| parent_group_id | a861046e-9cba-4f1a-ab2c-833d7e27c122 |
| port_range | |
| remote_security_group | |

Finally, you can launch your first instance with the name `my_first_instance` with the following command:

```
$ openstack server create --flavor m1.tiny --image 'CirROS 0.3.4' \
--security-group default --nic net-id=Network1 \
--availability-zone nova my_first_instance
```

This will launch your instance. To see details about it you can use the following command to show it in a list of instances running:

```
$ openstack server list
```

| ID | Name | Status | Networks |
| :--- | :--- | :--- | :--- |
| 4d33f633-bfff... | my_first_instance | ACTIVE | Network1=10.190.0.6 |

For more details, including information about the instance failing to launch for any reason, you can use the following:

```
$ openstack server show my_first_instance
```

You can also replace the name of the instance with the instance ID if you somehow end up with more than one instance with the same name.

Finally, you should try to log in to the instance via SSH. The address of the machine will be in a different network name space than your server, so you will have to SSH from a network name space shared by the instance. Get a list of name spaces with:

```
$ sudo ip netns
gdhcp-94d79735-dd56-4f5f-bf4e-13a13b7c67dc
grouter-7fe37ec8-a038-43a6-812c-22b3b02f87ac
```

Now using the netns exec command, we'll use the grouter network space to SSH into the server. Looking at the Networks column from the openstack server list command and SSH to that address as the cirros user. When it prompts for a password, use the default of cubswin:) (the closing parenthesis is part of the password).

```
$ sudo ip netns exec grouter-7fe37ec8-a038-43a6-812c-22b3b02f87ac \
ssh cirros@10.190.0.6
cirros@10.190.0.6's password:
$
```

This prompt, with just the $, will be on the CirrOS instance you launched. You can poke around this filesystem to see what's running—not much! In Chapter 6, “Private Compute Cloud,” you'll learn more about what you can do with an instance, like assigning floating IP addresses and running services. Everything that works there will work here as well. We have a floating IP address pool and the resources to upload more images.

To wrap up, delete the instance. This action cannot be undone:

```
openstack server delete my_first_instance
```

## Summary

In this chapter, you learned how to configure a non-production deployment of OpenStack on a controller and compute node. Going through these commands manually provided you with a greater understanding of how OpenStack services fit together but which is abstracted away when you use DevStack or configuration management tools like Puppet.

# Deployments

In the following chapters, you are given examples of several types of OpenStack deployments to consider. Each deployment is based on a series of real-world scenarios that will be described in detail and followed up with instructions for how the deployment can be constructed in a small scale.

# 5
Foundations for
Deployments

> *Enter these enchanted woods,*
>
> *You who dare.*
>
> George Meredith, *The Woods of Westermain*

As has been discussed, an OpenStack deployment is made up of a series of components that come together, and of these components, there are key services that are used in most installations. All installations will require identity services provided by Keystone. Most deployments, including those demonstrated in subsequent chapters, will require networking services provided by Neutron, compute services provided by Nova and the RabbitMQ queuing service.

This chapter covers how to get your foundation of identity, networking, compute and queuing configured so that you can move on to build the rest of your infrastructure using Puppet.

## Requirements

For configuration of your systems you will need to satisfy the same requirements as you needed to for Chapter 4, “Your First OpenStack.” You need a single system (virtual or physical) as a controller node and a single system as a compute node.

Our recommended minimum specifications for a basic two-system setup of OpenStack are as follows:

- Controller Node—1 x 64-bit processor, 4GB of memory, 30GB of storage and two Network Interface Cards (NICs)

You will also want to prepare a compute node now:

- Compute Node—1 x 64-bit processor, 2GB of memory, 20GB of storage and one NIC

## Why Do I Need Two Nodes?

You have read here, and perhaps elsewhere, that the bare minimum for a production OpenStack cloud is two nodes. But why?

- **Scalability**—It’s very natural for some portions of your OpenStack deployment to scale beyond a single machine. Like the Compute Node, your Compute Node is the host to the virtual machines so that can often be the first node that you’ll want to have more of as your pool of users grow and you need to offer more resources. The Controller node can easily handle the functions for these additional Compute nodes.
- **High-availability**—In a mature, production OpenStack environment, you want your machines to be highly available (HA). By starting your first deployment as a two-node deployment, you are already making logical splits in your architecture which lend themselves to being made highly available. You may learn that you want nearly identical Controller Nodes for redundancy, but may not want or need the same in some of your other nodes at the same rate.
- **Security**—While service isolation is not the panacea for security, it does help. Privilege escalation from within instances of all types is a sadly common vulnerability and protecting your other services from this by keeping them on separate machines is important.

If you are configuring the Compute Node and wish to launch more than a couple small compute instances, you will want to give it more resources. Keep in mind, in the case of virtualization, you will also need to leave some resources for the host system.

## Caution

The default configuration we’re using in this book for OpenStack makes the HTTP-accessible dashboard (Horizon) accessible from any address. Many of the API endpoints are also accessible. While you do need authentication, the default passwords that we ask you to change are simple.

For the sake of security, when you’re setting this up initially as a demonstration consider using a local area network (LAN) for these systems and don’t allow SSH or HTTP access from the outside world. Networking can get complicated for newcomers to OpenStack, and you want to make sure you’re working in a trusted environment.

If you do choose to use cloud-based systems or other publicly accessible servers rather than local Virtual Machines or hardware, please keep security in mind as you work with OpenStack and take appropriate precautions with standard Linux access controls and firewalls. Remember, it’s very common for these providers to leave SSH and HTTP access available by default, and that’s precisely what you want to protect.

## Reference Deployment

As we covered in Chapter 4, this book provides a reference deployment using a pair of virtualized nodes using KVM. This can be found in Appendix A, “Reference Deployment.”
