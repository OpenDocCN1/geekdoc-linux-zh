
11. Now create your compute node, with 2G of RAM and 1 NIC:

```bash
$ sudo virt-install --connect qemu:///system -n compute --vcpus=2 -r 2048 \
--network=bridge=virbr0 --f /var/lib/libvirt/images/compute.qcow2 \
-c /var/lib/libvirt/images/ubuntu-14.04.4-server-amd64.iso --vnc \
--noautostart --os-type linux --os-variant ubuntu/trusty
```

With both servers up and running, you can log into them via ssh or interact through Virtual Machine Manager (see Figure A.1) to set up the systems as defined in Chapter 5, “Foundations for Deployments,” and beyond.

### Recommendations

Instead of interacting through Virtual Machine Manager for all your commands, you may want to install the `openssh-server` package on all systems. This will allow you to use SSH to connect to the machines and will make pasting commands into them easier.

Additionally, the Firefox web browser comes with the Ubuntu desktop you have installed. You can use this to interact with Horizon, the OpenStack Dashboard, without installing any additional software.

![](img/8684900d708748f86bb043faa5589f9e_262_0.png)

Figure A.1 Virtual Machine Manager. You can access the KVM instances you created by using Virtual Machine Manager.

## B Other Deployment Mechanisms

In this book we explored using Puppet to do various deployments of OpenStack. However, Puppet is just one of your options in the vast OpenStack ecosystem. By having a variety of deployment mechanisms, OpenStack can be deployed in your organization without a switch in tooling or by having it run on different tooling than the rest of your environment.

All deployment mechanisms that are part of the OpenStack community itself can be found by browsing through the OpenStack code repository at https://git.openstack.org/cgit/openstack/.

The tools covered here are the most popular and mature, but this list of tools is always changing, and it’s always worth doing a search for your favorite tool not listed here to see if there are OpenStack deployment instructions available or in development.

### Chef

Chef cookbooks are available for OpenStack under the OpenStack project in the project git repository. They all begin with the prefix `cookbook-openstack-` and end with the specific project they are deploying. For instance, you will find the compute (Nova) project Chef cookbooks via this address: https://git.openstack.org/cgit/openstack/cookbook-openstack-compute/tree/.

The `README.rst` file in each repository provides a reference for each project. Each of them has some basic instructions about usage of the cookbooks and many link to an additional repository that describes how to use it in the context of a full OpenStack deployment.

### Ansible

A series of Ansible playbooks are also available in the OpenStack project git repository, directly accessible for browsing from here: https://git.openstack.org/cgit/openstack/openstack-ansible/tree/.

Unlike Chef and Puppet, Ansible has provided a single deployment playbook that pulls in other components. Instructions for basic setup are included in the `README.rst` file, which includes a tour of some of the scripts available, depending on what kind of deployment you're looking to do, from boot-strapping to running playbooks individually and more.

### SaltStack and Others

Other open source configuration management tools, such as SaltStack, also now have published OpenStack tooling in their official repositories. These are maintained outside of the direct OpenStack community, and instructions for download and usage can be found by searching the code repositories and documentation for these projects.

### Vendor-Specific

Community-driven efforts with technologies such as Puppet, Chef and Ansible have come up to speed for production use in the recent past, but OpenStack had historically been complicated to deploy. As discussed in Chapter 14, "Vendors and Hybrid Clouds," vendors offer a vast array of vendor-specific deployment mechanisms. Some of these mechanisms are tightly integrated with what the vendor calls their own OpenStack distribution, which packages a lot of other tools in with their OpenStack offering. Red Hat and HPE are among companies with offerings. Other companies focus on using their deployment tools to focus on deployment, such as Juju by Canonical for the Ubuntu ecosystem.

The OpenStack Marketplace, hosted by the OpenStack Foundation, provides a comprehensive list of vendors who offer their own OpenStack distributions and appliances at http://www.openstack.org/marketplace/distros/.

![](img/8684900d708748f86bb043faa5589f9e_265_0.png)

## C Long-Lived Puppet

For each deployment example in this book we ran a setup script and then `puppet apply` to apply the manifests. This works well for working through each scenario to get a feel for how OpenStack works in various deployments, but it is not a maintainable way to run OpenStack. In order to take the Puppet deployments module and Hiera from this book and turn it into a real Puppet OpenStack deployment, there are some things that you will need to consider and changes that will need to be made.

### Puppet Master or Masterless?

From the Puppet side, the first main thing you'll need to change is that you might not want to run Puppet using `puppet apply` like we have here. Although some OpenStack deployments use masterless Puppet, it has some disadvantages. First, all Puppet code and Hiera data needs to be copied to every node and kept up-to-date. You also cannot use things like exported resources (https://docs.puppet.com/puppet/latest/reference/lang_exported.html) with masterless Puppet. Compared to masterless, running Puppet with a Puppet master has a few advantages as well. First, it provides a single place to make a change and have it automatically deployed out to every node. By default, all the clients will request a catalog and do a Puppet run every 30 minutes. This means that within 30 minutes, updates that can be applied and hand-made changes will be auto-reverted (as long as the resource that is changed is managed by Puppet). Although masterless Puppet also has some advantages too, such as no catalog compile bottleneck, you need to at least affirm that you want to be running masterless and weigh the pros and cons before you productize the solution provided in this book.

### Hiera

In this book we use a key/value tool called Hiera from Puppet to store preferences for each deployment example. For simplicity reasons, the Hiera used in this book barely meets the definition of what Hiera is supposed to be. Hiera is supposed to allow over-lapping values that are exposed based on a hierarchy. In this book we have a simple flat file. In any real deployment you will want to have a real hierarchy that exposes layers like region, node type, and whether the node is dev, staging, or prod. Think of a case where you might want your dev compute box to have a different version of a package than a production node. This is what Hiera is for. It can even be used to separate nodes geographically. A node in Europe will have different NTP and DNS servers than a node in the Americas. Read more about the power of Hiera at https://docs.puppet.com/hiera/1/.

### Passwords in Hiera

Another issue you will need to solve is storing passwords in Hiera. Checking passwords into git unencrypted is not a good idea and is unsafe. Using the `hiera-eyaml` back end is one solution to this problem. The passwords will be encrypted on disk and decrypted for catalog compiles (see: https://puppet.com/blog/encrypt-your-data-using-hiera-eyaml). This has the drawback that your Puppet master will need a decryption key but is a large improvement over plain text. There are other solutions to consider as well. Just keep in mind that managing passwords that hold the keys to your entire deployment should be a top consideration. Hiera includes passwords for the OpenStack admin user, RabbitMQ, and MySQL, any of which, if leaked, would be extremely dangerous.

### Node Classification

As noted earlier, in this book you are choosing what type of node you have by manually running `puppet apply` on a given box. This method does not scale well and is error prone. What would happen to your OpenStack cluster if someone accidentally applied the `foundations_public_cloud.pp` catalog to a compute host? In order to run this in production you need to first think about how you will do your Puppet node classification (https://docs.puppet.com/pe/latest/puppet_assign_configurations.html). This can be done using the Puppet console that ships with Puppet Enterprise (paid), but it can also be done with Hiera and the `site.pp` file. This is something you’ll need to consider as you productize this code.

### Module Management

One major consideration will be how you manage Puppet modules and stay in-sync with upstream. The versions of the modules are managed by the Puppetfile and then pulled by the Puppet deployment toolset r10k. For the most part, the Puppetfile shipped with this book puts you in good shape. Versions of non-OpenStack modules are locked to specific tags, which means that their code cannot "move" unless you move it. But new modules are tagged and released every day. In fact, many of the tags in that Puppetfile are probably already outdated. What system will you have for updating those tags and tracking new releases? How will you test the new modules? These are key considerations that you will need to make. I advise that falling behind and then trying to do a massive jump on all the modules at once is not a good plan. Plan on reviewing the module tags at least every few months to see if they can be upgraded. The following is an example of a module pinned to a tag:

```ruby
mod 'stdlib'
  :git => 'https://github.com/puppetlabs/puppetlabs-stdlib.git'
  :ref => '4.6.0'
```
