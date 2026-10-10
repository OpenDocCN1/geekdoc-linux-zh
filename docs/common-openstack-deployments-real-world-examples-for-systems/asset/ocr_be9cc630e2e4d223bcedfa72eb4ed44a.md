the openrc credentials. This is an outside module called openstacklib that is not part of our deployments module.

# Glance Profile

The profile for Glance, the imaging service, is where you start getting very interesting configuration options:

```
`$ cat /etc/puppet/modules/deployments/manifests/profile/glance.pp`

class deployments::profile::glance{
  $cirros_version = '0.3.4',
}
{
  include ::glance
  include ::glance::api
  include ::glance::registry
  include ::glance::keystone::auth
  include ::glance::backend::file
  include ::glance::db::mysql
  include ::glance::notify::rabbitmq

  glance_image { 'cirros':
    location  => "https://download.cirros-cloud.net/5/${cirros_version}/${cirros_version}-x86_64-disk.img",
    name      => "CirrOS ${cirros_version}",
    is_public => 'Yes',
    container_format => 'bare',
    disk_format => 'qcow2',
  }
}
```

This calls out to the OpenStack Glance module to pull in various components. In our profile we’re making a few decisions about how we want this basic configuration to work. We’re pulling in the API and Registry for Glance. We’re then making sure we have Keystone and MySQL for Glance set up to interact with our existing Keystone and MySQL services. Puppet makes this very easy, but you can see how it’s done manually back in Chapter 4 if you’d like a refresher. Finally, we’re also using the storage backend “file”, which is the default type of backend end for Glance and means it’s storing images on a filesystem. By default, they are stored in /var/lib/glance/images/ which is where you will find images you upload to Glance. Glance has the option of using different back ends, like the OpenStack Object Storage service (Swift) or Amazon’s S3. We have a single image configured in the installation, a very small and simple Linux-based operating system called CirrOS. As you can see, this profile defines which version of CirrOS will be used as our initial image in Glance as well as various details about it.

If you’re interested in further details about the OpenStack Glance module for the Mitaka release, you can browse it on your node filesystem or online:

+   - **Filesystem**—/etc/puppet/modules/glance/
+   - **Online**—https://git.openstack.org/cgit/openstack/puppet-glance/tree/?h=stable%2Fmitaka