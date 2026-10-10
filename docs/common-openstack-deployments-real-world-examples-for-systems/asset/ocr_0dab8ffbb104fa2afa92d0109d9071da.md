With these packages installed, you will now have an `/etc/nova/nova.conf` configuration file that will need several changes. The `[DEFAULT]` section will need the following (remember to replace 192.168.122.2 with the actual IP address of your controller):

```
my_ip = 192.168.122.2
rpc_backend = rabbit
auth_strategy = keystone
use_neutron = True
firewall_driver = nova.virt.firewall.NoopFirewallDriver
```

Next, remove `ec2` from the `enabled_apis` line, so it only has the following:

```
enabled_apis=osapi,compute,metadata
```

Now, switch from SQLite to MySQL in new `[database]` and `[api_database]` sections by adding:

```
[database]
connection = mysql://nova: NOVA_DB_PASSWORD@controller/nova
[api_database]
connection = mysql://nova: NOVA_DB_PASSWORD@controller/nova_api
```

In a new `[oslo_messaging_rabbit]` section put the following, where `RABBIT_PASSWORD` is the password you set up when installing the rabbitmq-server package earlier in the chapter:

```
[oslo_messaging_rabbit]
rabbit_host = controller
rabbit_userid = openstack
rabbit_password = RABBIT_PASSWORD
```

# Oslo

We’re using this Oslo_messaging_rabbit section here. What’s Oslo?

Named after the Oslo Peace Accord with the intent to “bring peace” to the OpenStack project, the Oslo project was created to develop a series of shared libraries for common solutions that many OpenStack projects need. For instance, most need to parse configuration files, generate log files and use a messaging queue. Rather than each project solving these in different ways with their own code, projects are encouraged to use Oslo.

As the OpenStack project has grown, so has Oslo. It now also includes solutions for caching, concurrency, policy enforcement, internationalization (i18n) features, database connectivity and more. For a full listing of all the shared libraries now provided, see http://governance.openstack.org/reference/projects/oslo.html.

And in a new `[keyystone_authtoken]` section add the following, using the password you were prompted for while setting up the nova user in place of `NOVA_PASSWORD`:

```
[keystone_authtoken]
auth_uri = http://controller:5000
auth_url = http://controller:35357
```