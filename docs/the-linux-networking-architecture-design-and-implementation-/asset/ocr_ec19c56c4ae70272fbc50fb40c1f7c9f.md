# 2.4 Kernel Modules 25

```
# Aliases - specify your hardware
alias eth0 wlan_cs
options wlan_cs eth=1 network_name="MyNet" station_name="neo"
alias char-major-4 serial
alias char-major-5 serial
alias char-major-6 lp
alias char-major-9 st

alias tty-1ldisc-1 slip
alias tty-1ldisc-3 ppp
```

FIGURE 2-5
Configuration file of the module loader: /etc/modules.conf.

**Loading Modules Automatically** In addition to the command-line tools described above, kernel modules can also be loaded into the kernel automatically when needed. To enable the automatic loading of modules, the corresponding support has to be activated when creating the kernel (CONFIG_KMOD).

Using the tools in the previous section to add and remove modules requires a user's intervention—more specifically, the intervention of root. For security reasons, only the system administrator is authorized to load and remove kernel modules. Though this approach is secure, it is somewhat inflexible—for example, when a user requires the functionality of a module that is currently not loaded in the kernel. For this reason, a means was created for reloading modules automatically into the kernel upon demand.

Normally, the kernel generates an error message when a resource or a specific driver is not registered. You can ask for this in advantage by use of the kernel function request_module(). To use this, you have first activate the option Kernel Module Loader when configuring the kernel. Request_module() will then try to use the probe command to automatically reload the desired module (and any additionally required modules). You can select options in the file /etc/modules.conf.

Figure 2-5 shows an example of the configuration file /etc/modules.conf. This file specifies that the network device eth0 is currently represented by the module wlan_cs and, for loading of this module, the specified parameters should be passed to this module. If probemod cannot find the module, then printk() generates an error message (See Appendix B.1.1.)

Though this mechanism runs in the configuration files, to ensure that no user can load system-critical modules. Modules loaded automatically can also be removed automatically after some time. More configuration options of the Kernel Module Loader and the probemod tool are described on the main pages and in [RuCo01].

# 2.4.2 Registering and Unregistering Module Functionality

In contrast to an application that runs its tasks after its start, a module normally provides functions used by other parts of the kernel in the course of the system operation. The kernel is enhanced by a new functionality, which may be removed after its use is.