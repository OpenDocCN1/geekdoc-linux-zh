complete as the command line clients, it does have all the features for basic administra-
tion and manipulation of your OpenStack environment and instances.
As we've seen in previous chapters, the dashboard is opened by using your web browser
to navigate to the IP address of your controller. If you're using the reference deployment
from Appendix A, "Reference Deployment," this can be done on your host machine
where you run the controller and compute VMs from. Otherwise you'll just need to make
sure the machine you run the browser from can access the IP address that the controller
is running on.

# **Add a Flavor**

A flavor defines the amount of R AM and disk (root, ephemeral and swap), as well as
the number VCPUs to be allocated to an instance. By default, there are several flavors
defined that are useful for most deployments (see Figure 6.2). These flavors are com-
pletely customizable. In order to add a flavor, you will need to log in as the admin user.

> **Note**
> Since the minimum requirements we defined for our deployment are so low, you will not
> be able to use all of the default flavors.

Most of the columns in this list are pretty straightforward if you're familiar with
Linux filesystems: VCPUs are the number of processors for the guest, R AM is mem-
ory, Root Disk is the storage that the base image with root filesystem is copied to, and
Swap Disk is the swap space on the system. Setting the flavor as public means that it's
available to all the projects on the system. The less obvious columns include Ephemeral

![](bbox=[0.13, 0.62, 0.95, 0.93])

Figure 6.2  List of default flavors