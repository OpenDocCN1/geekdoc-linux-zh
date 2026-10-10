
class { '::neutron::agents::ml2::ovs':
  bridge_mappings => $bridge_mappings,
  bridge_uplinks => $bridge_uplinks,
}

You see some network-specific information regarding network and subnet hashes and routers, which you may have edited while updating the hiera/common.yaml file. We’re also bringing up the secondary Ethernet interface (eth1) on the controller and handling bridges.

If you’re interested in further details about the OpenStack Neutron module for the Mitaka release, you can browse it on your node filesystem or online:

- **Filesystem** — /etc/puppet/modules/neutron/
- **Online** — https://git.openstack.org/cgit/openstack/puppet-neutron/tree/?h=stable%2Fmitaka

### RabbitMQ Profile

Finally, the RabbitMQ queuing profile is the simplest of all. It could have been included elsewhere, but we have it as a separate profile in case there is a need to add or tune anything about the service.

```
$ cat /etc/puppet/modules/deployments/manifests/profile/rabbitmq.pp
class deployments:profile:rabbitmq
{
  include ::rabbitmq
}
```

This uses the RabbitMQ Puppet module installed by setup.sh to set up and install RabbitMQ. You will have set a rabbit_password in the hiera/common.yaml, and this file also handles several other configuration options defined by our RabbitMQ deployment.

### Testing the Controller Node

When your puppet apply command from earlier is complete, you will want to run some test commands to make sure everything was created properly and running. Let’s start with some basic functionality of MySQL. The default password and hostname are stored in the root user’s ~/.my.cnf file, so you can just run the following to see that the databases for Glance, Keystone, Neutron and Nova were created. In these example commands, we’ve included some sample output, which won’t match exactly but will give you some idea what to look for.

```
$ sudo -H mysql -e "show databases;"
+--------------------+
| Database           |
+--------------------+
| information_schema |
| glance             |
| keystone           |
| mysql              |
| neutron            |
| nova               |
| performance_schema |
+--------------------+
```

You may also want to inspect the tables that were created, say, for Glance:

```
$ sudo -H mysql '-e show tables;' glance
| Tables_in_glance |
|------------------|
| artifact_blob_locations |
| artifact_blobs |
| artifact_dependencies |
| artifact_properties |
| artifact_tags |
| artifacts |
| image_locations |
| image_members |
| image_properties |
| image_tags |
| images |
| metadef_namespace_resource_types |
| metadef_namespaces |
| metadef_objects |
| metadef_properties |
| metadef_resource_types |
| metadef_tags |
| migrate_version |
| task_info |
| tasks |
```

The preceding command can also be run against the Nova, Neutron and Keystone databases to see their tables.

Next, let's see that the OpenStack services are responding properly to the test user. To do this, we'll first want to pull in credentials from our test openrc file, then we can run each command.

#### Tip

As you explore OpenStack commands you'll quickly learn that they often provide a lot of detail. We've worked to format it legibly in this book, but if you're struggling to read it, the command output for many of these commands is included in a GitHub repository for scripts and configurations sorted by chapter at [https://github.com/DeploymentsBook/scripts-and-configs](https://github.com/DeploymentsBook/scripts-and-configs).

```
$ source /etc/openrc.test
$ openstack flavor list
+----+---------+-----+-----+-------------+-------+----------+
| ID | Name    | RAM | Disk | Ephemeral | VCPUs | Is Public |
+----+---------+-----+-----+-------------+-------+----------+
|  1 | m1.tiny |  512 |   1 |           0 |     1 |      True |
|  2 | m1.small| 2048 |  20 |           0 |     1 |      True |
|  3 | m1.medium|4096 |  40 |           0 |     2 |      True |
|  4 | m1.large| 8192 |  80 |           0 |     4 |      True |
|  5 | m1.xlarge|16384| 160 |           0 |     8 |      True |
```

```
$ openstack network list -c ID -c Name

| ID | Name |
| --- | --- |
| aaca0d44-a9fd-4fa9-9ed2-984c547c1539 | ext-net |
| cd293246-5f09-4232-8e96-d70091234c56 | Network1 |
```

```
$ openstack image list

| ID | Name |
| --- | --- |
| cdf2e591-3b16-4bd1-9bd6-a2560e739492 | Cirros 0.3.4 |
```

Now that you have confirmed that the test user is working properly, you can run a couple commands that only the administrator can run, first by sourcing the admin rc file so you are using the correct credentials.

```
$ source /etc/openrc.admin
$ openstack role list

| ID | Name |
| --- | --- |
| 38e23d9c84eb46049286976efb93bdee | _admin |
| 9fe2ff9ee4384b189a490878d3e92bab | member |
| c9c9e53b68f6e4859e3d9e82e0f6edda | SwiftOperator |
```

```
$ openstack user list

| ID | Name |
| --- | --- |
| 067124f893ac4e9382fa2d099b1a9504 | glance |
| 33c6b93cf0caf49d0fb631a98969d3577 | admin |
| 84fb1b3cba4844b40fe653c312f2a6277 | nova |
| 88572aa29c1c641d95bcb12f79804f49 | neutron |
| f7fa77ea833c4d4d3d212fcf875f3eec | test |
```

Finally, let’s confirm that Open vSwitch (OVS) is working properly. The output of the following command should look similar to this with stanzas for bridges br-int, br-ex and br-tun:

```
$ ovs vs-vac21 show
f5b2d445-5c9d-42b7-88c6-1e90e1cfdfac
Bridge br-int
    fail_mode: secure
Port br-int
    Interface br-int
        type: internal
Port int-br-ex
    Interface int-br-ex
        type: patch
        options: {peer=phy-br-ex}
Port patch-tun
Interface patch-tun
  type: patch
  options: {peer=patch-int}
Port 'tab035/7edc-72'
  tag: 1
Interface 'tab035/7edc-72'
  type: internal
Port 'qr-584feae2-79'
  tag: 1
Interface 'qr-584feae2-79'
  type: internal
Bridge br-tun
fail_mode: secure
Port patch-int
Interface patch-int
  type: patch
  options: {peer=patch-tun}
Port 'vxlam-c0a8*abf'
Interface 'vxlam-c0a8*abf'
  type: vxlan
  options: {df_default=true*, in_key=flow, local_ip='192.168.122.9*', out_key=flow, remote_ip='192.168.122.191*'}
Port br-tun
Interface br-tun
  type: internal
Bridge br-ex
Port phy-br-ex
Interface phy-br-ex
  type: patch
  options: {peer=int-br-ex}
Port 'qq-576e34l8-87'
Interface 'qq-576e34l8-87'
  type: internal
Port br-ex
Interface br-ex
  type: internal
Port 'eth1'
Interface 'eth1'
  ovs_version: '2.5.0'
```

Sometimes OVS isn't properly running after it is either freshly installed or the node is rebooted. This is a known bug with OVS. Restarting the OVS service resolves it, though you wouldn't want to do this in production without planning.

```
$ sudo service openvswitch-switch restart
```

Now you will want to log into the Horizon dashboard, which is opened by using your web browser to navigate to the IP address of your controller. If you're using the reference deployment from Appendix A, accessing the dashboard can be done on your host machine where you run the controller and compute VMs from. Otherwise you'll just need to make sure the machine you run the browser from can access the IP address that the controller is running on.

![](img/8684900d708748f86bb043faa5589f9e_138_0.png)

Figure 5.1. Horizon dashboard login page

#### Tip

Which IP address? The controller has two NICs, but only one of them has an address you can navigate to. This is the one assigned to eth0 and would have been allocated when you installed the controller.

Once you have a login screen (see Figure 5.1), you want to log in with username "test" and the test password you created when editing the hiera/common.yaml file.

If all of these commands worked, congratulations! You now have a running controller node. If you have errors, first go back and check your configuration to make sure you didn't skip a step. If that doesn't help, see the troubleshooting section later in this chapter for some resources to help you debug.

You'll now want to set up the other server, the compute node.

## Compute Node

You are now creating a Compute node. The compute node will be the host of all of the compute Instances that you create. As discussed, it is important for security and performance to keep these separate from all of the tooling used to run OpenStack itself. We will configure the compute node in much the same way as we did the controller. First edit several variables in the default hiera common.yaml at /etc/puppet/hiera/common.yaml. Open with your preferred text editor using sudo and make similar changes to what you did in the controller file. Save the file.

#### Reminder

Don't skip editing hiera/common.yaml. These values need to sync up with what you used on the controller. Plus, the defaults are easy to guess and are stored on a public git repository.
