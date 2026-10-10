# Nova

Installation of Nova on the controller will closely mirror the previous instructions for Glance, with registration with Keystone and configuration file changes prior to testing. However, this time we'll be creating two MySQL databases: nova and nova_api. Use your favorite MySQL tool, or create them via the command line.

```
$ mysql -u root -p
> CREATE DATABASE nova;
> GRANT ALL PRIVILEGES ON nova.* TO 'nova'@'%' IDENTIFIED BY
'NOVA_DBPASSWORD';
> CREATE DATABASE nova_api;
> GRANT ALL PRIVILEGES ON nova_api.* TO 'nova'@'%' IDENTIFIED BY
'NOVA_DBPASSWORD';
> quit
```

Create the credentials in Keystone for the Nova user and service and add the API endpoints. As before, remember the value you enter when prompted for a nova password, since it will need to be used in the configuration files.

```
$ source /etc/openrc.admin
$ openstack user create --domain default --password-prompt nova
User Password:
Repeat User Password:
```

| Field | Value |
| :----- | :----- |
| domain_id | f2e5f2b8ab0694a3cbf43734eb6bcc3ae |
| enabled | True |
| id | 3e3fd33ce015449799bde64af7e630931 |
| name | nova |

```
$ openstack role add --project service --user nova admin
$ openstack service create --name nova --description \
"OpenStack Compute" compute
```

| Field | Value |
| :----- | :----- |
| Description | OpenStack Compute |
| enabled | True |
| id | 6d8da6185a234ed032931e05eca75 |
| name | nova |
| type | compute |

```
$ openstack endpoint create --region RegionOne compute \
public http://controller:8774/v2.1/$(tenant_id)s
```

| Field | Value |
| :----- | :----- |
| enabled | True |
| id | f0f82d91d7b04d59a024ebd6c5acedb1 |
| interface | public |
| region | RegionOne |
| region_id | RegionOne |
| service_id | aee3db3fcf5741d7b92f44678b9ba9d |
| service_name | nova |
| service_type | compute |
| url | http://controller:8774/v2.1/$(tenant_id)s |