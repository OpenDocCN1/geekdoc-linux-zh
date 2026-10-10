# **OpenStack Components 67**

> > **Tip**
> > Tired of environment variables? You can also pass this data into your environment within the openstack command with the following (when prompted for a password, it is the admin password you set):
> > $ openstack --os-auth-url http://controller:5000/v3 --os-project-domain-name default \
> > --os-user-domain-url default --os-project-admin --os-username admin \
> > --os-auth-type password token issue

# ### OpenStack Client

At this point we can pause and complete the creation of the openrc files mentioned earlier that will contain the echo statements we used above. First, let’s create /etc/openrc-admin with the following contents. We’re using ADMIN_PASSWORD as a placeholder for the admin user password you set earlier:

```
```bash
export OS_PROJECT_DOMAIN_NAME=default
export OS_USER_DOMAIN_NAME=default
export OS_PROJECT_NAME=admin
export OS_USERNAME=admin
export OS_PASSWORD=ADMIN_PASSWORD
export OS_AUTH_URL=http://controller:5000/v3
export OS_IDENTITY_API_VERSION=3
export OS_IMAGE_API_VERSION=2
```
```

Now we’ll create /etc/openrc-test with similar information. Here, TEST_PASSWORD should be replaced with what you specified when creating the test user.

```
```bash
export OS_PROJECT_DOMAIN_NAME=default
export OS_USER_DOMAIN_NAME=default
export OS_PROJECT_NAME=test
export OS_USERNAME=test
export OS_PASSWORD=TEST_PASSWORD
export OS_AUTH_URL=http://controller:5000/v3
export OS_IDENTITY_API_VERSION=3
export OS_IMAGE_API_VERSION=2
```
```

> > **Warning**
> > All components depend upon Keystone. If you run into any problems configuring Keystone, debug the commands and configuration before moving forward with configuring other components.

# ### Glance

Glance is the image service for OpenStack. It provides a mechanism for uploading and indexing disk images that will be used to launch instances in OpenStack. The OpenStack API can then read the index of images in order to retrieve information about each so that it can be deployed later by Nova, the compute service.

Just like for Keystone, the Glance image service will be installed via the Ubuntu Cloud Archive, and we will need to create an empty database in MySQL for the Glance to use. Once again, you may create this empty database with a tool you like or with the following