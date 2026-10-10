If your organization is large enough that you can devote full-time staff to managing your OpenStack-driven environment, there are also vendors who specialize in training and consulting services. These services are valuable for when your team needs to learn more about a specific component of OpenStack or simply is seeking some solid expertise to get over some kind of hurdle you're facing.

The OpenStack Foundation maintains a Marketplace to find vendors at http://www.openstack.org/marketplace/. This marketplace also provides a tour of some of the distributions and appliances that are built around OpenStack and seek to make deployment and management easier. These distribution offerings almost always need vendor interaction for you to explore, but there are some that offer community editions or other simplified samples of their products if you wish to explore them on your own.

In earlier chapters we used Puppet to deploy OpenStack. Some vendors use these open source Puppet modules or others covered in Appendix B, "Other Deployment Mechanisms," but oftentimes they have built their own or added on top of the open source options. It's valuable to ask how they're doing a deployment, so you can become familiar with their tooling so you know how the pieces are coming together.

Beyond just deployment mechanisms, as you explore the vendor ecosystem you should keep in mind that you'll likely be moving into other proprietary software components. The base is still OpenStack, but the tooling around it will likely be something developed or licensed by the vendor to provide value to their customers over their competitors. It's important to understand this as you get into licensing agreements, so you can make the appropriate decisions along with your legal department.

# Public and Hybrid Clouds

Beyond simply running OpenStack on your own, you can become a user of OpenStack clouds by exploring public clouds or leveraging a hybrid cloud environment in your organization.

# Public Clouds

The OpenStack Marketplace mentioned earlier has a section completely devoted to public clouds. As discussed in depth in Chapter 7, "Public Compute Cloud," a public cloud is run by a third party, and you are able to interact with it to spin up instances (typically virtual machines), add block storage to your instances, interact with object storage or manage networking between your instances. It may even be somewhat transparent to you that you're using OpenStack, aside from your familiarity with the user-level tooling, as administration of OpenStack itself is handled by the vendor.

With the capability to simply hook in to a public cloud without handling maintenance and scaling, this is a very compelling option for many organizations. Public clouds can get you the ability to grow exponentially and leverage the services OpenStack provides without a large up-front investment or making it a core competency of your organization. As you evaluate the options, there are several points to keep in mind centered around location, cost and data sovereignty and security.