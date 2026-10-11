
## 03 Installation on agents and post-installation

On all the agent nodes, you now need to run the following command:

```bash
$ sudo apt-get install puppet
```

This will install Puppet and an init script (`/etc/init.d/puppet`) for running the Puppet agent daemon. With this, we complete the installation process but Puppet is not started yet. Let's now configure the master and the agents, so they can talk to each other as and when required. The first step in this process is to set the master's name and certificates. You will need a DNS server that can resolve the names to corresponding IP addresses, then in the main section of the master's `puppet.conf` file, set the `dns_alt_names` setting to a comma separated value of each hostname that master can have. The default name to which an agent will try to connect is **puppet**. So, if you use "puppet" as the hostname for master, it will save you some effort. This is one of the most important steps and should be done carefully to avoid communication issues at later stages.

## 04 Activate certificates

The next step is to activate the certificates on the master. If this is the only Puppet master in your deployment, or if it will be acting as the CA server for a multi-master site, you should now run the following:

```bash
$ sudo puppet master --verbose --no-daemonize
```

This will create the CA certificate and the Puppet master certificate, with the appropriate DNS names included. As soon as the terminal output displays:

> Notice: Starting Puppet master version 3.8.3.

...kill the process by typing Ctrl+C, because we don't want the master to run. Now put all the Puppet manifests and modules in place and then configure a web server if you are planning to use Puppet to manage configuration loads.

## 05 Configure the agent

First of all, you will need to configure the `puppet.conf` settings in each of the agent nodes so that they are able to connect to your Puppet master server. Also, certain environment-specific factors should be changed according to your infrastructure requirements. Then you will need to start the Puppet agent service. You can either configure it to start on boot or set up a cron job, so that it runs at specific intervals. To start the Puppet service, type:

```bash
$ sudo puppet resource service <NAME>
ensure=running enable=true
```

Then configure the cron job using:

```bash
$ sudo puppet resource cron puppet-agent \
ensure=present user=root minute=30 command=/usr/\
bin/puppet_agent --onetime --no-daemonize --play
```

The final step is to sign the certificates for each of the agent nodes. Note that in an agent/master deployment, an admin must approve a certificate request for each agent node before the node can fetch configurations. Agent nodes will request certificates the first time they attempt to run. To approve the requests, log on to the Puppet master server and view outstanding requests using:

```bash
$ sudo puppet cert list
```

Then sign a request by typing:

```bash
$ sudo puppet cert sign <NAME>
```

You can also sign all the requests in one go using:

```bash
$ sudo puppet cert sign --all
```

With this, the agent nodes are now ready to communicate with the master. Puppet also enables a higher level of configuration by letting you classify the nodes. With this, you can determine which agent nodes receive which information from the master.

![](img/0fc17bd4c29dc437e3ac28a53f7559db_22_0.png)

![](img/0fc17bd4c29dc437e3ac28a53f7559db_22_1.png)

## Run when file updates

You can run a command automatically whenever a file changes. Just use an exec resource with `refreshonly` set to `true`, for example:

```ruby
file { "/etc/bind":
  source => "/dist/apps/bind"
}

exec { "/usr/bin/ndc reload":
  subscribe => File["/etc/bind"],
  refreshonly => true
}
```

![](img/0fc17bd4c29dc437e3ac28a53f7559db_22_2.png)

## Feature

## DEVOPS

## MANAGE YOUR VIRTUAL MACHINES WITH VAGRANT

Vagrant makes it easy for you to manage several virtual machines in one go. Here we will learn how to install and get started with Vagrant.

Before diving further into what Vagrant can do for you, let's first understand what Vagrant is. In simple terms, Vagrant provides an easily configurable, reproducible and portable work environment, built on top of virtualisation technology. The work environment built by Vagrant can be controlled by a single consistent workflow in order to help maximise the productivity and flexibility.

To achieve its magic, Vagrant stands on the shoulders of giants like VirtualBox, VMWare, AWS, or other providers. You can then use provisioning tools – such as shell scripts, Chef or Puppet – to automatically install and configure software on the machine. So, once you create a single Vagrantfile, you just need to `vagrant up` and everything is installed and configured for you to work with. Other members of your team can create their development environments from the same configuration, so whether you're working on Linux, OS X or Windows, all your team members are running code in the same environment, against the same dependencies, all configured the same way.

## Installing Vagrant

Vagrant can be easily downloaded and installed on your system. Go to the Vagrant downloads page (vagrantup.com/downloads.html) and download the package appropriate for your system. You can then install it by following the standard installation procedure for your platform. Also, the installer automatically adds the `vagrant` command to your system path, so you can start using it now. If you see the "command not found" error, just log out and back in, and it should work.

## Vagrantfile

A Vagrantfile describes the type of machine required for a project, and how to configure and provision these machines. Note, that the actual filename for the file is simply Vagrantfile. Vagrant runs with one Vagrantfile per project, and the Vagrantfile is supposed to be committed to version control. This enables other developers involved in the project to check out the code, run `vagrant up` and be on their way. Vagrantfiles are portable across every platform Vagrant supports.

## Environment variables

You can use environment variables in Vagrantfile, by calling `ENV[variable_name]`. For example:

```ruby
config.vm.box =
"#{ENV['boxname']}"
```

## VAGRANTFILE EXPLAINED

```ruby
# File, Edit, View, Search, Require, Help
# -*- mode: ruby -*-
# vi: set ft=ruby:
Vagrantfile API: 2.x/5.x
VERSION = "2"

#Check if you have the good Vagrant version to use docker provider...
Vagrant.require_version ">= 1.6.0"
vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
# All Vagrant configuration is done here. The most common configuration
# options are documented and commented below. For a complete reference,
# please see the online documentation at vagrantup.com.
ENV["VAGRANT_DEFAULT_PROVIDER"] = "docker"

# Share an additional folder to the guest VM. The first argument is
# the path on the host to the actual folder. The second argument is
# the path on the guest to mount the folder. The optional third
# argument is a key of non-specific options.
config.vm.synced_folder ".", "/vagrant_data"
# Provider-specific configuration so you can limit-tune vm (for
# backing providers for Vagrant. These expose provider-specific options.
# Example for VirtualBox:
# config.vm.provider "docker" do |d|
#   d.has_ssh = "*"
#   d.has_ssh = true
# end

config.ssh.port = 22
end

'Vagrantfile' 31 lines, 1879 characters
```

## VAGRANTFILE VERSION CHECK

Docker is only supported on Vagrant version 1.6 and above, so before anything else, you need to confirm if the installed Vagrant has the proper revision. You can do this easily, as shown here.

## VAGRANT DEFAULT PROVIDER

Setting up the Vagrant default provider saves having to specify at every Vagrant command that the provider is Docker. The rest of the file has options that Vagrant will use to build the Vagrant machine and run a container.

## PROVIDER-SPECIFIC CONFIGURATION

Once the provider is set, more configurations specific to the provider. This is done in Vagrantfile using a loop. This way, multiple config vm.provider blocks can exist to configure multiple providers.

## SSH SETTINGS

The settings within config.ssh.set how Vagrant will access your machine via SSH. The default is fine, and even if this line were not added, SSH should have used its default port 22. But, this shows you can change the port.
