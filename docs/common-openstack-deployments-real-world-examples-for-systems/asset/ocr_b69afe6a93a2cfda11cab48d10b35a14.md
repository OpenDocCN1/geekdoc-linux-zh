![](bbox=[0.24, 0.11, 0.7, 0.31])

Figure 11.3    Containers, Nodes and Bays

# ## Installing Magnum

The Magnum Puppet modules for Mitaka were still being developed and tested at the time of writing, so there will soon be a Puppet-driven way to configure Magnum for your infrastructure. As of writing, the best way to try out Magnum is to deploy our Foundations framework discussed in Chapter 5, "Foundations for Deployments," with a custom Compute node that will use Magnum.

# # Summary

Containers are a popular topic and OpenStack has met the challenge head-on. It started off by supporting container-specific Nova compute drivers from a very early date. The Magnum project, which we gave a quick tour of, then brought in more comprehensive support for the common container technologies out there today, including Docker, Kubernetes and Apache Mesos.