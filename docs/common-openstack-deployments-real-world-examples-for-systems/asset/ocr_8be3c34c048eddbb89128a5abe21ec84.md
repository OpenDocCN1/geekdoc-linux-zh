# Exploring the Deployment: Command Line Client

As you’ve learned, the OpenStack Client (OSC) can do everything that the Horizon dashboard can and more. The System Information screen in the dashboard is very similar to what you see when listing services with OSC:

```
```
$ source /etc/openrc.admin
$ openstack service list
```
```

| ID | Name | Type |
| --- | --- | --- |
| 2fb5afa87bba5482cbf31ae606daac9c26 | keystone | identity |
| 3c1c214c93e3aa4fe62da8b2f34de5c9d3 | Compute Service v3 | computev3 |
| 3d5f410362f07462b3a5355ef604c02b7c23 | Image Service | image |
| 88dcf889462f433a9b9355e604c02b78a | neutron | network |
| 9e8ac41f598dc483f81f2a166f2d052df2 | cinder | volume |
| ae28d23d39044447ae6341ddc804de9c7b | cinder v3 | volumev3 |
| b4d823a8e89474cd4acc54ebb3517b0e0 | ceilometer | metering |
| b9bdc44e8113e481981e33820745e369a | cinder v2 | volumev2 |
| f4afe8dc46eef47f5948f8cfe610182292b | swift | object-store |
| f73b98720cd54fb9b47075a7593d09911 | Compute Service | compute |

Run this command with --long to get even more information about each service running and a view that’s even more similar to the dashboard.

You can also list the Ceilometer meters once you have an instance running with **ceilometer meter-list** and refer back to Chapter 7, “Public Compute Cloud,” to refresh your memory on polling other statistics. In this chapter we added Cinder, so if you’ve created some volumes you’ll see a new volume size meter to work with. For Swift, if you’ve created a container and uploaded objects, you’ll see new meters like **storage.objects** and **storage.objects.size**.

Being proficient with OSC is an important part of administering a deployment. With this whole cloud deployment, do some similar instance launches and shutdowns of instances. Refer back to previous chapters to create a block storage volume and mount it on an instance, create a container and add some files to it for reference in your instances. Or come up with your own project to do or experiments for how far you can push this deployment scenario as you familiarize yourself with the tooling. See Appendix E, “OpenStack Client (OSC),” and the development documentation with a command listing for more OSC commands at http://docs.openstack.org/developer/python-openstackclient/command-list.html.

# A Bigger Cloud

As you become more familiar with OpenStack and start planning your own deployment you’ll grow your cloud well beyond the pair of servers we’ve been working with. You’ll also need to make sure your services are reliable and secure, and eventually you’ll likely want to add more services than we’ve covered.