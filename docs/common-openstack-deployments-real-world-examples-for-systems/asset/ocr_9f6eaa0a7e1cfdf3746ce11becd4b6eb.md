We’ll now move away from Neutron configuration files and back over to Nova. We need to add a `[neutron]` section in our `/etc/nova/nova.conf` that contains the following (remember, the `metadata_proxy_shared_secret` from the `metadata_agent.ini` earlier):

```
```python
[neutron]
auth_url = http://controller:53535/v3
username = http://controller:9696
auth_plugin = v2password
project_domain_name = default
project_name = service
user_domain_name = default
username = neutron
password = NEUTRON_PASSWORD
  ova_bridge = br-int
region_name = RegionOne
timeout = 10
  extension_sync_interval = 600
service_metadata_proxy = True
metadata_proxy_shared_secret = something_secret
```
```

Restart your nova services to be sure all your configuration changes have been picked up:

```
```bash
$ sudo service nova-api restart
$ sudo service nova-consoleauth restart
$ sudo service nova-scheduler restart
$ sudo service nova-conductor restart
$ sudo service nova-novncproxy restart
```
```

As discussed in Chapter 3, we’ll be using a series of OVS bridges for the deployment. Most of these are set up automatically by Neutron, but we do need to manually add the address for your external bridge, `br-ex`:

```
```bash
$ sudo ovs-vsctl add-br br-ex
$ sudo ovs-vsctl add-port br-ex eth1
```
```

The final step is adding details to Neutron about your networks. As we go through these commands, you may want to refer back to Figures 3.5 and 3.6 from Chapter 3, which give you a detailed view into these interfaces and networks.

```
```bash
$ neutron net-create ext-net --router:external \\
    --provider:physical_network br-ex --provider:network_type flat \\
    --shared
```
```

Created a new network:

| Field | Value |
|---|---|
| admin_state_up | True |
| availability_zone_hints |  |
| availability_zones |  |
| created_at | 2016-05-17T02:56:07 |
| description |  |
| id | 3016c117-052d-44e8-8115-ce929cc0c266 |
| ipv4_address_scope |  |
| ipv6_address_scope |  |
| is_default | False |