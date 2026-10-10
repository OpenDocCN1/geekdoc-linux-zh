some traditional technology companies have taken to building public clouds. These typically are offered alongside their other offerings or in concert with their private cloud offerings.

During one OpenStack summit keynote, a company talked about how their customers are now using hybrid clouds, which blend a deployed series of private clouds alongside a public cloud. This company will go on-site to assist with the deployment of a private cloud, and then offer a public cloud for the public-facing components of their infrastructure.

# Web Hosting Company

Companies that have specialized in web hosting have also begun offering public compute options. Many of these companies began by offering the purchase of a Virtual Private Server (VPS) to customers and also offer specific hosted services such as blogs or forum installations. With the move to cloud, these hosting companies have empowered their users to build their own applications using a framework similar to that which many of these traditional web hosting services have run off of.

Additionally, some companies are leveraging portions of OpenStack for their customers by offering object storage for individual files, which you’ll learn about in Chapter 9, “Object Storage Cloud.”

# Requirements

In this deployment scenario you’ll be using the controller and compute nodes you created in Chapter 5, “Foundations for Deployments.” For this installation, you can use the same systems you used in Chapter 6, since we did not make any additions to that deployment beyond the foundation.

You may also want to set aside some time to let this deployment sit running. Since the metering collected by OpenStack is tracked over time, having a couple instances running over night will collect data so you can explore the next day or the next week.

# Select Components

On top of the foundational tooling, we’ll be adding the Ceilometer telemetry service to your deployment in this scenario. This will extend the basic installation to have to include following services, placement of which is demonstrated in Figure 7.1:

+   - Compute (Nova)
+   - Identity (Keystone)
+   - Networking (Neutron)
+   - Image service (Glance)
+   - Dashboard (Horizon)
+   - Ceilometer (Telemetry)