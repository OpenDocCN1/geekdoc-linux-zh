As we walk through deployment scenarios in the following chapters, specific uses will be detailed to provide examples and a taste for the flexibility of OpenStack.

# ## Key Components

OpenStack is built from a series of components that are developed as their own projects within the OpenStack community. The following is a quick summary of each of the terms that will be referenced in the deployments throughout this book.

# ### Instances

With the exception of storage and bare-metal focused deployments, you will need to be familiar with instances in OpenStack. Instances are typically Virtual Machines (VMs) using an underlying VM technology that you may be familiar with such as KVM or gemu, VMware or Hyper-V. However, as you will learn in Chapter 11, “Controlling Containers,” there has been a push to provide stronger support of containers in OpenStack. Whether they are VMs or containers, they are referred to as instances in OpenStack.

# ### Queuing

Before getting into specific OpenStack project components, it's important to talk about how the services interact with each other. At the most basic level, OpenStack services interact through a series of APIs that each project supports. Calls to these APIs are handled by a messaging queue that is installed early in an OpenStack installation. All interactions go through the queue so that processing can be reliable and predictable, happening in the order in which they were issued and providing a buffer when there is a spike in usage so that none of the commands issued get lost. In order to interact with this queuing system, most post requests directly, but you will notice that a small subset of the OpenStack components also run with a scheduling daemon.

# ### Dashboard (Horizon)

Horizon is the web-based dashboard for OpenStack that provides an interface for both OpenStack administrators and users of the platform. It enables administrators and operators to manipulate various settings related to users, servers, quotas and more. The dashboard is also easily customizable by organizations and cloud operators who wish to add their own branding to the dashboard. The capabilities of Horizon expand as OpenStack continues to grow and add features with each release.

The interface for administrators provides the capability to manipulate users, view system information and adjust defaults and much more (see Figure 1.1).

By contrast, the user dashboard shown in Figure 1.2 is a user-facing view that enables individual users to control their virtual machines, networking configuration and components made available to them by an administrator.