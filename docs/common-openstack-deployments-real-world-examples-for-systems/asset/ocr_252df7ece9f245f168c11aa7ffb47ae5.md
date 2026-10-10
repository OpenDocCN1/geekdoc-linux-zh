```
$ openstack ip floating create ext-net
```

| Field | Value |
|---|---|
| fixed_ip | None |
| id | d8c6592-efc2-450e-9726-ccf91d1a05c2 |
| instance_id | None |
| ip | 203.0.113.10 |
| pool | ext-net |


We can use this one we just created for this new instance by running the following, and then check to make sure the IP was assigned.

```
$ openstack ip floating add 203.0.113.10 ferret
$ openstack server list
```

| ID | Name | Status | Networks |
|---|---|---|---|
| 41887a02-lefa-4b4d-8fe4-d31c68da066e | ferret | ACTIVE | Network\xl=10.190.0.13, 203.0.113.10 | 


Voila! The instance now has both a private address and the newly assigned 203.0.113.10 address. This address can be used to SSH into the system from another system on this network.

# Running a Service

Whether you used the OpenStack dashboard (Horizon) or OpenStack Client (OSC) to bring up your first instance, you're now all set to start logging into your server and making changes.

# Logging in with SSH

The Ubuntu cloud image that we're using does not have a default password to go with the default ubuntu user, so accessing it is done with an SSH key that you imported or created in an earlier step. Now you'll want to use this key and log in.

First, you will need to interface with the system that has the gateway address of 203.0.113.1 defined. If you're using instructions from Appendix A, this will be the host machine where your controller and compute VMs run. You can either SSH to this machine, or use a Terminal on the Ubuntu desktop on that machine directly to SSH into your instance. To see if your instance is accessible from the machine you're on, we can start out with a ping test. Look up what 203.0.113.0/24 address your machine has, and then use the ping command to test. For example if your address is 203.0.113.9 use the following command, which should get pings back from the server:

```
$ ping -c 5 203.0.113.9
PING 203.0.113.9 (203.0.113.9) 56(84) bytes of data.
64 bytes from 203.0.113.9: icmp_seq=1 ttl=63 time=3.56 ms
64 bytes from 203.0.113.9: icmp_seq=2 ttl=63 time=1.35 ms
64 bytes from 203.0.113.9: icmp_seq=3 ttl=63 time=1.50 ms
64 bytes from 203.0.113.9: icmp_seq=4 ttl=63 time=1.46 ms
64 bytes from 203.0.113.9: icmp_seq=5 ttl=63 time=1.58 ms

```