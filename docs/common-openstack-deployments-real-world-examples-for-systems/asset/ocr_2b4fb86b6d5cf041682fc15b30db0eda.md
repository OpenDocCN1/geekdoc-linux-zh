# **Neutron**

Perhaps one of the most complicated sections of an OpenStack deployment to configure is the networking service, Neutron. Earlier in the chapter we configured several Open vSwitch bridges and virtual connectors that will be important here. First, we’ll need to create a MySQL database and user like we’ve done for all the other services:

```
```
$ mysql -u root -p
> CREATE DATABASE neutron;
> GRANT ALL PRIVILEGES ON neutron.* TO 'neutron'@'%' IDENTIFIED BY 'NEUTRON_DBPASSWORD';
> quit
```
```

Configure Neutron with the Keystone identity server. Remember the password you put in when prompted; you’ll need this later for the configuration file.

```
```
$ source /etc/openrc.admin
$ openstack user create --domain default --password-prompt neutron
User Password:
Repeat User Password:
```
```

| Field | Value |
|---|---|
| domain_id | 2262f2b8aB093a43cbbf4373486bc03ae |
| enabled | True |
| id | f0e6a17a78f34132acdfd6755c8b4f54 |
| name | neutron |

```
```
$ openstack role add --project service --user neutron admin
$ openstack service create --name neutron --description \
'OpenStack Networking' network
```
```

| Field | Value |
|---|---|
| description | OpenStack Networking |
| enabled | True |
| id | 213ed845959864a1872ddbc56040a0ad |
| name | neutron |
| type | network |

```
```
$ openstack endpoint create --region RegionOne network \
public http://controller:9696
```
```

| Field | Value |
|---|---|
| enabled | True |
| id | 01a5628811c84583acf8010115a0210e |
| interface | public |
| region | RegionOne |
| region_id | RegionOne |
| service_id | 213ed845959864a1872ddbc56040a0ad |
| service_name | neutron |
| service_type | network |
| url | http://controller:9696 |