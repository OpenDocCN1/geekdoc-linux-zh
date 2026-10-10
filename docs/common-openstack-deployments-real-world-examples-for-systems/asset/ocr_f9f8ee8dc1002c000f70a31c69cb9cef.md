# Horizon Profile

The Horizon dashboard profile is very simple since no special code outside of the upstream puppet module is required in order for the dashboard to run.

```
$ cat /etc/puppet/modules/deployments/manifests/profile/horizon.pp

class deployments::profile::horizon
{
    include ::apache
    include ::horizon
}
```

It runs Apache, so we're pulling in a generic Apache module and it also needs the OpenStack Horizon module.

If you're interested in further details about the OpenStack Horizon module for the Mitaka release, you can browse it on your node filesystem or online:

+   - Filesystem—/etc/puppet/modules/horizon/
+   - Online—https://git.openstack.org/cgit/openstack/puppet-horizon/tree/?h=stable%2Fmitaka

# Keystone Profile

With the Keystone identity profile, we're getting complicated again.

```
$ cat /etc/puppet/modules/deployments/manifests/profile/keystone.pp

class deployments::profile::keystone
{
    include ::apache
    include deployments::profile::users
    include ::keystone
    include ::keystone::cron::token_flush
    include ::keystone::roles::admin
    include ::keystone::endpoint
    include ::keystone::db::mysql
    include ::keystone::apache
}
```

Since Keystone uses WSGI to run the service, it also requires the Apache module and also a specific keystone::wsgi::apache class. In addition, it pulls in several other components of the Keystone Puppet module, including a cron job, administrative role information and configuration for the endpoint. Finally, you edited the hiera/common.yaml to change the passwords for the admin and test users, that was defining what "deployments::profile::users" brings in.

> **Note**
> 
> In Chapter 4 you may recall that we configured Keystone with Fernet tokens. This is where the community recommendations are trending and was easy to do in our manual deployment. However, support for Fernet tokens came out somewhat recently, in the Kilo release. It is not yet default in OpenStack. For our Puppet-driven deployment scenarios we're still using the current default—UUID tokens.