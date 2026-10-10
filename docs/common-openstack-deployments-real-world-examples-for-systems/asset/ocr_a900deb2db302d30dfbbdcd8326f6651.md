You can also replace the name of the instance with the instance ID if you somehow end up with more than one instance with the same name.

Finally, you should try to log in to the instance via SSH. The address of the machine will be in a different network name space than your server, so you will have to SSH from a network name space shared by the instance. Get a list of name spaces with:

```
$ sudo ip netns
gdhcp-94d79735-dd56-4f5f-bf4e-13a13b7c67dc
grouter-7fe37ec8-a038-43a6-812c-22b3b02f87ac
```

Now using the netns exec command, we'll use the grouter network space to SSH into the server. Looking at the Networks column from the openstack server list command and SSH to that address as the cirros user. When it prompts for a password, use the default of cubswin:) (the closing parenthesis is part of the password).

```
$ sudo ip netns exec grouter-7fe37ec8-a038-43a6-812c-22b3b02f87ac \\
ssh cirros@10.190.0.6
cirros@10.190.0.6's password:
$ 
```

This prompt, with just the $, will be on the CirrOS instance you launched. You can poke around this filesystem to see what's running—not much! In Chapter 6, “Private Compute Cloud,” you'll learn more about what you can do with an instance, like assigning floating IP addresses and running services. Everything that works there will work here as well. We have a floating IP address pool and the resources to upload more images.

To wrap up, delete the instance. This action cannot be undone:

```
openstack server delete my_first_instance
```

# ## Summary

In this chapter, you learned how to configure a non-production deployment of OpenStack on a controller and compute node. Going through these commands manually provided you with a greater understanding of how OpenStack services fit together but which is abstracted away when you use DevStack or configuration management tools like Puppet.