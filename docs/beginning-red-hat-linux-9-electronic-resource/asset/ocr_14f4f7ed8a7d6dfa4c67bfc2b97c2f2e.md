If we check the box against a network interface in the **Trusted devices** section, this configures the firewall to allow all traffic to and from that interface (because we trust all the machines connecting via that interface). However, can we be sure that one of these machines has not been compromised and that the packets coming from it are the work of a hacker?

The other options on the dialogue enable us to allow incoming connections on a selection of well-known ports for different services. For example, let’s pretend that our example machine will be running a Web server, and we’ll need remote access via ssh for administration, so the WWW and SSH boxes need to be checked. This ends up looking like this:

![](bbox=[0.29, 0.25, 0.73, 0.64])

When we press the OK button, the firewall configuration is updated and saved so that the machine will reboot with the new configuration in place.

# ## Lokkit

There is another tool that we can use to configure the firewall on our Red Hat Linux systems. It’s called Lokkit (installed from the gnome-lokit RPM). It is a simple to use configuration tool that asks a series of simple questions and configures the firewall according to the answers you supply. It’s not as versatile or powerful as the method we’ve just discussed, so we’ll make no more mention of it here.

> > Note that Lokkit is not meant for custom firewall configuration and has fewer options than the Red Hat redhat-config-securitylevel tool.