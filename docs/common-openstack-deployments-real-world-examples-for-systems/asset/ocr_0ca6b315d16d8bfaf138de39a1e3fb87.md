```
$ openstack endpoint create --region RegionOne compute \
> internal http://controller:8774/v2.1/%(tenant_id)s
```

| Field     | Value                                                        |
| --------- | ------------------------------------------------------------ |
| enabled   | True                                                         |
| id        | f879688639174ad689e645143f9ee8e8                               |
| interface | internal                                                     |
| region    | RegionOne                                                    |
| region_id | RegionOne                                                    |
| service_id| aee3db3dcf5741d7b922446768c8ba9d                             |
| service_name | nova                                                       |
| service_type | compute                                                    |
| url       | http://controller:8774/v2.1/%(tenant_id)s                   |

```
$ openstack endpoint create --region RegionOne compute \
> admin http://controller:8774/v2.1/%(tenant_id)s
```

| Field      | Value                                                        |
| ---------- | ------------------------------------------------------------ |
| enabled    | True                                                         |
| id         | 476096b7ad4b4888b6d5c9b7170bb601                               |
| interface  | admin                                                        |
| region     | RegionOne                                                    |
| region_id  | RegionOne                                                    |
| service_id | aee3db3dcf5741d7b922446768c8ba9d                             |
| service_name | nova                                                       |
| service_type | compute                                                    |
| url        | http://controller:8774/v2.1/%(tenant_id)s                   |

With the service user and endpoints created, now install the packages. For Nova there are several more that you need to install than for Keystone and Glance:

```
$ sudo apt-get install nova-api nova-conductor nova-consoleauth \
> nova-novncproxy nova-scheduler
```

# Basic Pieces of Nova

Glance just had a couple services, but Nova has a whole lot of them. The following is a quick rundown of the services you are installing now:

+   • **API**---Just like with other OpenStack services, the API is how you interact with the service, including activities such as launching a new instance or asking for details about one already running.
+   
+   • **Conductor**---A daemon that enables OpenStack to function in an isolated manner so that compute nodes don’t need to directly access the database.
+   
+   • **Consoleauth**---Provides access via a VNC-style console in an instance, either from the outside or directly via something like Horizon, the OpenStack dashboard.
+   
+   • **Novncproxy**---As with consoleauth, this proxy daemon is also required for access to the console on an instance.
+   
+   • **Scheduler**---A daemon that takes an instance creation request from the queue and determines which compute server a host should run on.