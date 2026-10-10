
The final lines of this file use the Puppet module's capability to configure a test volume. For simplicity's sake we use this setup_test_volume, which creates a simple 10GB file mounted to a loopback (by default, /dev/loop2) device and added to LVM as a single logical group. An init file is also created in our cinder.pp profile to make sure the file is mounted and the volume group is activated if your controller reboots.

> ### Note
>
> What Is LVM? The official page for LVM is at: http://www.sourceware.org/lvm2/ and there are various resources and how-tos available for free online, particularly for basic control.

Once your puppet apply command completes, you're ready to start creating volumes and attaching them to instances!

## Creating and Attaching a Volume: Dashboard

We will begin with the process for creating and attaching a volume using the OpenStack dashboard (Horizon). With the block storage (Cinder) component now installed, when you log into the dashboard with your test user you will see a section for Volumes in the left under Project in Compute, as shown in Figure 8.3.

![](img/8684900d708748f86bb043faa5589f9e_186_0.png)

Figure 8.3 Empty, default Volumes page in the dashboard

### Creating a Volume

On this page you'll want to click on the Create Volume button, which will bring up a dialog like the one in Figure 8.4 where you will put in information about the volume you wish to create. Some fields will be automatically filled out, but the rest will be up to you.

The volume name is what you will be using to refer to the volume. A description is optional and can be used for whatever you want, maybe as a reminder to yourself about what the volume is intended for. The volume source enables you to pre-populate the volume with a source of defined data. By default, it queries the Image Storage (Glance) service and enables you, as one of the options, to put an Image on your newly created volume. You may also want to create a volume source that has a basic filesystem and partition table for your new volume so it doesn't need to be created later after you mount it on an instance. For this scenario, we will just use No source, empty volume and will explain how to partition and format it after it is added to an instance.

The type of volume will inform the scheduler as to which type of storage back end you need to use. From the customer point of view, you want to define a type as tiered and varied storage with different properties, like how fast the storage device is, Quality of Service (QoS) requirements or whether a tier has replication. Prices may vary for the customer based on which options they select. From your perspective, this means one of these tiers may be using Ceph and another a proprietary NAS device that has the desired qualities for the tier being offered. We have not set a volume type, so it will remain as “No volume type” for this example. Our device only has 10GB, so we'll start out in this test by creating a 1GB volume to attach to our instance. The availability zone is identical to the one in compute (Nova) and currently must match the zone where the instance you wish to attach it to resides. In our deployment scenario we only have a single availability zone, so the default of nova should remain selected.

![](img/8684900d708748f86bb043faa5589f9e_187_0.png)

**Figure 8.4** Create a volume in the dashboard.

![](img/8684900d708748f86bb043faa5589f9e_188_0.png)

Figure 8.5 A volume called "walrus" has been created.

When you have finished, you can click on Create Volume in order to begin volume creation. You will be returned to the Volumes page of the dashboard, which will show your new volume as you can see in Figure 8.5.

### Attaching a Volume

A volume on its own is not of much value, so we'll now want to attach it to a compute instance. If you do not have an instance running, you can create a basic one with a CirrOS image now in the Instances dashboard. Refer back to Chapter 6 if you need a refresher on the steps to create an instance.

Attaching a volume in the dashboard is done by going to the drop-down menu on the right side of where your volume is listed. From that menu, select Manage Attachments to bring up the screen, where you can attach the volume to an instance (Figure 8.6).

In this example we have an instance running called "giraffe" and the UUID is also included, since names can be reused in compute (Nova). There is also an optional Device Name section where you can define what you want the device to be named when it's attached to the instance. This can safely be left blank and a name will be assigned automatically. When you're done selecting the instance to attach to, click on Attach Volume.

![](img/8684900d708748f86bb043faa5589f9e_189_0.png)

Figure 8.6 Managing volume attachments

When the volume completes attaching, you will be able to see it in the dashboard as “Attached to” with the instance name and the device it has shown up as (see Figure 8.7).

![](img/8684900d708748f86bb043faa5589f9e_189_1.png)

Figure 8.7 A volume has been attached.

You’ll next want to log into the instance to see that the device has been attached successfully, but this process is the same whether you’re completing this process with the dashboard or through the command line. You can continue to learn the process for attaching a volume using the OpenStack Client on the command line, or skip to the “Using the Volume” section later in this chapter to see what you can do to use your new volume.

## Creating and Attaching a Volume: OpenStack Client

As we’ve discussed previously, the dashboard can be a convenient way to interact with OpenStack to complete most of the simple operations you may need to do. You will find, however, that most operators prefer using the command line clients or SDKs to interface with the tooling. As such, we’ll now walk through the same process we did with the dashboard but instead using the OpenStack Client (OSC).

The OSC is small and can easily be run from any system that has access to the API endpoints for the services. In our deployment scenarios, this means it must be on the same network as your controller node. You must also have access to the /etc/openrc test file that was created on your controller and compute nodes, so for these commands we will assume you’re running everything on your controller.

### Creating a Volume

We will be using the test user in order to create this volume, since it will also be attaching to a compute instance owned by the test user. To begin, we’ll bring the environment variables for the test user in from the openrc file. Then you can issue the command to create a 1GB volume using that storage back end. Aside from the name, we will be using the same specifications for creation of the volume as was used with the OpenStack dashboard (Horizon), which means creating a 1GB volume that is empty (no partition table, filesystem or data) and is in our default availability zone, called nova.

> **Tip**
>
> You’ll notice that OpenStack commands often output a lot of detail that doesn’t fit well on the pages of a book. A GitHub repository of much of this command output sorted by chapter is available at https://github.com/DeploymentsBook/scripts-and-configs.

```
$ source /etc/openrc test
$ openstack volume create --size 1 --availability-zone nova seagull
```

| Field | Value |
|-------|-------|
| attachments | [] |
| availability_zone | nova |
| bootable | false |
| consistencygroup_id | None |
| created_at | 2016-04-15T04:19:46.086611 |
| description | None |
| encrypted | False |
| id | 5372cc5-087a-4342-a67b-377477a14af2 |
| multiattach | False |
| name | seagull |
| properties | |
| replication_status | disabled |
| size | 1 |
| snapshot_id | None |
| source_volume | None |
| status | creating |
| type | None |
| updated_at | None |
| user_id | aa47b986f3734f66b331784241fa15a |

To confirm this volume has been created, you can run a command to list the volumes (Listing 8.1).

As you can see, both the walrus and the seagull volumes are listed here since they were both created in this chapter. The walrus volume is showing that it is attached to the giraffe instance.

If you need to make changes to a volume, use the `openstack volume set` command. Running that command alone will give you help output to assist you with making changes to all the parameters before the volume is attached.

### Attaching a Volume

As mentioned earlier, you can't do much with a volume if it's not attached to an instance. You'll now want to add your new volume to an instance. First you'll want to see what instances are available:

```
$ openstack server list
```

| ID | Name | Status | Networks |
|---|---|---|---|
| 8232827a-E106-4453-874D-4D21 ff2b2204 | giraffe | ACTIVE | private=10.0.0.3 |

With confirmation that you have an instance running, you can now run the command to attach the seagull volume to the giraffe instance:

```
$ openstack server add volume giraffe seagull
```

This command will have no output, but the next time you run `volume list` you will see that the volume has been attached (Listing 8.2).

Since the giraffe instance already had the walrus volume attached as `/dev/vdb`, you will notice that it has attached the seagull volume as `/dev/vdc`.

Congratulations, you have successfully added a Cinder block storage volume to an instance on the command line!

## Using the Volume

Whether you used the OpenStack dashboard or the command line to create and attach your volume, we will now want to actually confirm the volume was attached and then go ahead and use it with our instance. It may be easiest to use the console in dashboard in order to run the following commands, but if you followed instructions in an earlier chapter so that your CirrOS instance has been set up for SSH (Secure Shell), feel free to use SSH instead.
