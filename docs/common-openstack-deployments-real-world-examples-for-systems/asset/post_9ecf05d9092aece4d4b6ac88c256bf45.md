
vendors are available in the open source repositories. Each determines what features to support, but gives you the most direct support for the networking ecosystem that you may be working in.

- **Proprietary, vendor-specific** — Many vendors who charge for OpenStack deployments also have their own drivers and agents. You may run into these if you pay for a deployment.

When considering drivers, note that some of these are shipped with Neutron and others are packaged separately. Learn more about drivers for OpenStack at http://www.openstack.org/marketplace/drivers

## Compute (Nova)

For the purpose of our scenarios, the compute components outlined in Chapter 1 are broken up between two servers to offer service isolation.

On the controller node, you will have the nova-conductor, scheduler, api and api-metadata daemons. On the compute node where instances run, you will only have nova-compute. This isolation is to keep the privileged controller isolated from the instances that users run, and any privilege escalation vulnerabilities that may crop up with the virtualization technology being used.

Like Queuing and Networking, this compute node is used for all of our scenarios.

## Image (Glance)

When you want to boot an instance in OpenStack, one of the first things you need to do is select what operating system you wish to use. Glance is what holds those images and makes them available to the user, storing both metadata and images themselves on your local disk or a storage backplane.

The image service in our scenarios will serve up a default CirrOS image from the local disk. In a later chapter, you will be adding Ubuntu Server 14.04 as well (at the time of writing, Ubuntu 16.04 had just been released and we were unable to make time to test it).

## Dashboard (Horizon)

The Horizon dashboard offers a friendly, web-based interface for interacting with your OpenStack deployment, both as a user and as an administrator. All of our deployment scenarios will have the dashboard as a component.

## Foundation Scenario

Now that you have a basic environment set up, we want to set up your foundation, which is the basic Puppet module we’ve created to deploy a simple OpenStack controller. This foundation will be used in all subsequent chapters.

### Controller Node

In order to configure the controller node, you will first want to get familiar with the default Hiera common.yaml file. Hiera is a tool that stores a key/value combination that can then be referenced by Puppet. In these deployment scenarios, all modifications we're making to default OpenStack Puppet modules are stored in this common.yaml file.

The Hiera common.yaml file you will be working with was placed on your filesystem with the setup.sh script that was run earlier. You will find this file at /etc/puppet/hiera/common.yaml. Open with your preferred text editor using sudo and follow the instructions in the file for adding your IP addresses, passwords, tokens and secrets that you should change. Save the file.

> **Caution**
> Don't skip editing hiera/common.yaml.
> The IP addressing for your controller and compute node **must** be set to reflect your environment. Puppet will fail with errors if you don't set these variables, and using the defaults with 127.0.0.1 will not work with a multi-node installation.
> Pay attention to updating the passwords, too. Remember, these default authentication credentials live on a fully public git repository.

With these changes completed, we can finally run the commands to apply the Puppet manifest that will install the foundational components for you.

```
sudo puppet apply /etc/puppet/modules/deployments/manifests/role/foundations.pp
```

This command may take some time to run. As it runs, you'll see a lot of output that describes what Puppet is doing.

## Running puppet apply Again

The puppet apply command can be run multiple times. You may want to run it again if you need to make changes to the Hiera common.yaml for a setting or if you had a problem like loss of Internet access during a run or ran into other errors.
Though it shouldn't happen, if you do run into errors that cause your deployment scenario to fail, you can use the `--debug` flag to run the Puppet command in debug mode. This will provide more detailed output, which can help you determine what went wrong.
With this flag, your command would then be:

```
sudo puppet apply --debug /etc/puppet/modules/deployments/manifests/role/foundations.pp
```

This will be a lot of output. You can use pipe and tee to direct output to a file as well as showing it to you in STDOUT:

```
sudo puppet apply --debug \
  /etc/puppet/modules/deployments/manifests/role/foundations.pp | \
  tee ~/puppet_apply_foundations.log
```

This will create a puppet_apply_foundations.log in your home directory for you to go through later.

While it's running, take a look at what is included in the foundations.pp Puppet role:

```
$ cat /etc/puppet/modules/deployments/manifests/role/foundations.pp
class deployments::role::foundations {
 include deployments::profile::base
 include deployments::profile::glance
 include deployments::profile::horizon
 include deployments::profile::keystone
 include deployments::profile::nova
 include deployments::profile::neutron
 include deployments::profile::rabbitmq
 include ::mysql::server
}

include deployments::role::foundations
```

On the surface this is very simple, but we'll dig into it a bit more to explain how it works.

# Puppet Roles, Profiles and Modules

The OpenStack Puppet community maintains a series of open source Puppet modules for deploying OpenStack, which are used by this book. Modules are shared configuration tools that are generic enough for all kinds of organizations and companies to share them. They are loaded up in our deployment as a series of building blocks to create the deployment scenario you want. We also use a high level “deployments” module hosted on GitHub, which contains our roles and profiles.

We are using Puppet roles and profiles in order to organize the Puppet configuration of the OpenStack Puppet modules. By using roles and profiles we can create a series of files that define specific servers (roles) that contain similar things as defined in profiles, essentially gluing together the modules. As you can see in foundations.pp, it includes profiles like “base” which we will use in all of our scenarios.

You can tell the difference between roles and profiles inside of our deployments module and other modules in the configuration by looking at how they are included. However, the difference between roles and profiles is more than just their names. Roles are the “business-logic” definitions that encapsulate profiles. Profiles are the implementation definitions that encapsulate modules.

A role declaration in our deployments module will look something like this:

```
include deployments::role::foundations
```

You'll see this role included in foundations.pp. The role's puppet file includes itself to make them easier to consume.

A profile declaration is similar, but uses the deployments::profile prefix:

```
include deployments::profile::uca
```

Finally, when calling a module (or a component of a module) outside of our deployments module, you'll see something like:

```
include ::openstacklib::openstackclient
```

To learn more about roles, profiles and modules, visit the official Puppet documentation https://docs.puppet.com/. Several valuable articles and blog posts have also been written about them. Because they become dated quickly, use your favorite search engine to find the latest.

## Profiles

Each of these profiles configure a different component of your OpenStack deployment and you can dig into each one to learn what it’s configuring.

### Base Profile

The base profile is shared among all of our deployments.

```
$ cat /etc/puppet/modules/deployments/manifests/profile/base.pp
class deployments::profile::base {
include deployments::profile::openrc
include deployments::profile::ucc
include ::ntp
include ::openstacklib::openstackclient
# add an alias to /etc/hosts to ensure sudo works
host { ${::hostbase}:
ip => $::ipaddress,
}
}
```

It sets up the openrc files that we will use for credentials later in this chapter to run our OpenStack client commands. We’re adding the Network Time Protocol (NTP) configuration so time is kept synced on our systems and are also including installation of the OpenStack Client. The uca profile configures Ubuntu Cloud Archive (UCA). As explained in Chapter 1, we’re using the UCA in order to get the recent OpenStack release version, Mitaka, for the Ubuntu Long Term Support release we’re running, 14.04. Drilling down into this profile will show you that there’s a section where the $release is defined. This is gathered from the Hiera common.yaml file and where set it to mitaka.

```
$ cat /etc/puppet/modules/deployments/manifests/profile/uca.pp
# Ubuntu Cloud Archive
class deployments::profile::uca {
$release,
$repo,
{
include ::apt
class { '::openstack_extras'::repo::debian:ubuntu':
release => $release,
repo    => $repo,
package_require => true,
}
Apt::Source{ | -> Package <|}
}
```

The final included section is the OpenStack Client (OSC), which we put on all of the systems so you can run OSC commands on whatever system you’re on, along with
