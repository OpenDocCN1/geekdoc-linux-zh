The final lines of this file use the Puppet module's capability to configure a test volume. For simplicity's sake we use this setup_test_volume, which creates a simple 10GB file mounted to a loopback (by default, /dev/loop2) device and added to LVM as a single logical group. An init file is also created in our cinder.pp profile to make sure the file is mounted and the volume group is activated if your controller reboots.

> ### Note
> 
> What Is LVM? The official page for LVM is at: http://www.sourceware.org/lvm2/ and there are various resources and how-tos available for free online, particularly for basic control.

Once your puppet apply command completes, you're ready to start creating volumes and attaching them to instances!

# ## Creating and Attaching a Volume: Dashboard

We will begin with the process for creating and attaching a volume using the OpenStack dashboard (Horizon). With the block storage (Cinder) component now installed, when you log into the dashboard with your test user you will see a section for Volumes in the left under Project in Compute, as show in Figure 8.3.

![](bbox=[0.08, 0.47, 0.88, 0.89])

Figure 8.3 Empty, default Volumes page in the dashboard