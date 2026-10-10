new guest would get renamed, a new MAC address generated for its network interface, and other modifications can be made depending on its intended use.

# ### The D-Bus Machine ID

Many Linux installations will utilize a machine identification number generated at install time, called the **D-Bus machine ID**. However, if a virtual machine is cloned to be used as a template for other virtual machine installations, a new D-Bus machine ID would need to be created to ensure that system resources from the hypervisor get directed to the appropriate guest system.

The following command can be used to validate that a D-Bus machine ID exists for the running system:

```
```
$ dbus-uuidgen --ensure
```
```

If no error messages are displayed, then an ID exists for the system. To view the current D-Bus machine ID, run the following:

```
```
$ dbus-uuidgen --get
17f2e0698e844e31b12ccd3f9aa4d94a
```
```

The string of text that is displayed is the current ID number. No two Linux systems running on a hypervisor should have the same D-Bus machine ID.

The D-Bus machine ID is located at /var/lib/dbus/machine-id and is symbolically linked to /etc/machine-id. Changing this ID number on a running system is discouraged as system instability and crashes are likely to occur. If two virtual machines do have the same D-Bus machine ID, follow the procedure below to generate a new one:

```
```
$ sudo rm -f /etc/machine-id
$ sudo dbus-uuidgen --ensure=/etc/machine-id
```
```

In the event that /var/lib/dbus/machine-id is not a symbolic link back to /etc/machine-id, then /var/lib/dbus/machine-id will need to be removed.

# ### Deploying Virtual Machines to the Cloud

There are a multitude of IaaS (*infrastructure as a service*) providers available that run hypervisor systems and that can deploy virtual guest images for an organization. Practically all of these