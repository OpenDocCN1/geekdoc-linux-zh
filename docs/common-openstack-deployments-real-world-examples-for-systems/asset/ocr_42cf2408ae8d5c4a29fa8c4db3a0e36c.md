```
#!/bin/bash

sudo apt-get update
sudo apt-get install -y puppet
sudo gem install --no-rdoc ri0k

sudo cp -a * /etc/puppet
sudo service puppet restart

cd /etc/puppet
sudo ri0k puppetfile install -v info
```

Let's run this script now. This should be run as your user, since it will invoke sudo as needed:

$ ./setup.sh

Running the setup script will take several minutes as it downloads the Ruby gems and required packages from the Ubuntu repositories. Once complete, you will have a Puppet-driven environment that you can then start running scenarios on.

# # Select Components

In Chapter 1, “What is OpenStack?” the components of OpenStack presented in this book were summarized. The following will explain how each are used with respect to our scenarios.

# ## Identity (Keystone)

Used for every scenario in this book, the Keystone identity service provides authentication and access management in OpenStack. A Keystone component will be added to every project your users interact with so that access controls can be set and enforced. Refer back to Chapter 4 for a detailed outline of how this is handled under Projects, Domains, Roles, Users and User Groups.

As an identity service, Keystone provides integration with popular authentication mechanisms such as various LDAP implementations, including Active Directory.

# ### Identity versus Authentication

An important and often confused component of Keystone are the concepts of “Identity” and “Authentication” when handling users.

Identity refers to identifying who is accessing specific cloud resources. This is typically a user.

Authentication refers to the act of verifying that a user is who they say they are. This is typically done through some sort of login by the user which is either managed by Keystone itself or passed on to a back end such as LDAP.

These components work together to fold into Access Management, or authorization, to determine what authenticated identities have access to each component.