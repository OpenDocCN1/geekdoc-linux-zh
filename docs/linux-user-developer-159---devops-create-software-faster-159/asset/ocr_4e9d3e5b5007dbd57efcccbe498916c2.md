# Feature

# DEVOPS

# MANAGE YOUR VIRTUAL MACHINES WITH VAGRANT

Vagrant makes it easy for you to manage several virtual machines in one go. Here we will learn how to install and get started with Vagrant.

Before diving further into what Vagrant can do for you, let's first understand what Vagrant is. In simple terms, Vagrant provides an easily configurable, reproducible and portable work environment, built on top of virtualisation technology. The work environment built by Vagrant can be controlled by a single consistent workflow in order to help maximise the productivity and flexibility.

To achieve its magic, Vagrant stands on the shoulders of giants like VirtualBox, VMWare, AWS, or other providers. You can then use provisioning tools – such as shell scripts, Chef or Puppet – to automatically install and configure software on the machine. So, once you create a single Vagrantfile, you just need to `vagrant up` and everything is installed and configured for you to work with. Other members of your team can create their development environments from the same configuration, so whether you're working on Linux, OS X or Windows, all your team members are running code in the same environment, against the same dependencies, all configured the same way.

# Installing Vagrant

Vagrant can be easily downloaded and installed on your system. Go to the Vagrant downloads page (vagrantup.com/downloads.html) and download the package appropriate for your system. You can then install it by following the standard installation procedure for your platform. Also, the installer automatically adds the `vagrant` command to your system path, so you can start using it now. If you see the "command not found" error, just log out and back in, and it should work.

# Vagrantfile

A Vagrantfile describes the type of machine required for a project, and how to configure and provision these machines. Note, that the actual filename for the file is simply Vagrantfile. Vagrant runs with one Vagrantfile per project, and the Vagrantfile is supposed to be committed to version control. This enables other developers involved in the project to check out the code, run `vagrant up` and be on their way. Vagrantfiles are portable across every platform Vagrant supports.

# Environment variables

You can use environment variables in Vagrantfile, by calling `ENV[variable_name]`. For example:

```
config.vm.box =
"#{ENV['boxname']}"
```

# VAGRANTFILE EXPLAINED

```
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

# VAGRANTFILE VERSION CHECK

Docker is only supported on Vagrant version 1.6 and above, so before anything else, you need to confirm if the installed Vagrant has the proper revision. You can do this easily, as shown here.

# VAGRANT DEFAULT PROVIDER

Setting up the Vagrant default provider saves having to specify at every Vagrant command that the provider is Docker. The rest of the file has options that Vagrant will use to build the Vagrant machine and run a container.

# PROVIDER-SPECIFIC CONFIGURATION

Once the provider is set, more configurations specific to the provider. This is done in Vagrantfile using a loop. This way, multiple config vm.provider blocks can exist to configure multiple providers.

# SSH SETTINGS

The settings within config.ssh.set how Vagrant will access your machine via SSH. The default is fine, and even if this line were not added, SSH should have used its default port 22. But, this shows you can change the port.