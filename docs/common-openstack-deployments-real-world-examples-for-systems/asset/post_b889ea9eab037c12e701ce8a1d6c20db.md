
## tcpdump

The tried and trusted `tcpdump` (<http://www.tcpdump.org/>) command is essential in the toolkit of any OpenStack administrator. It may be used for tracing the trickery to isolate provider network traffic going to and from the instances and various other things. Whether it's your physical interfaces or ones in the network name spaces, once you determine that you are unable to ping an instance or traffic is behaving inconsistently, you'll need to learn why. It can help you answer questions like “Where is traffic stopping?” and “Are specific types of traffic being blocked?” From there you can isolate which part of the network you need to troubleshoot.

A useful `tcpdump` command on `eth0` of your control interface may look like the following:

```
sudo tcpdump -i eth0 -vvv
```

While this is running, make sure you do something that should show output, like pinging the server you're running this on. Use Control-c to stop the capture. If traffic is running on the interface, you will likely see a great deal of traffic. Adjust this command as needed to listen on various interfaces. Remember, this can even be used in conjunction with the `ip netns exec` command to see traffic on the networks in name spaces.

> **Tip**
> Not a `tcpdump` guru yet? Learning how to read `tcpdump` output takes skill and experience. When you add in learning about how OpenStack uses networking, you may find yourself struggling.
> 
> Do yourself a favor. Save the output from `tcpdump` into a file and load it up in the graphical tool Wireshark (<https://www.wireshark.org/>). This tool gives you a visualization of the packets that were captured and enables you to drill into them. An example of a `tcpdump` command you can use with Wireshark is as follows:
> 
> ```
> sudo tcpdump -i eth0 -w packet_debug.pcap
> ```
> 
> As before, the interface you wish to listen on follows the -i flag, which you may want to change. The -w flag goes on to define the filename you're saving it to. Use Ctrl-c to stop the capture when you believe you have enough data.
> 
> You then load this `packet_debug.pcap` file into Wireshark for analysis. It's still not going to be easy until you get the hang of it, but it's easier than looking at the raw logs!

## MTUs

There was a section about maximum transmission unit (MTU) size in the networking chapter. As a reminder, if you find inconsistent behavior in how network traffic is flowing, such as you can ping an instance but SSH starts and times out during a handshake, you may want to look at the MTU size. Remember the diagram of the packet, and spend some time thinking about how your network is configured and what kind of encapsulation is happening to figure out what your MTU size should be.

Both the `tcpdump` command and the `ip` command can be of assistance in looking into MTU size issues. The `tcpdump` command can help you figure out where the packets get stuck. If used early enough in the life of the packet, like at an originating tap interface, tcpdump can help you figure out how large the packet is early on. The `ip link -s` command can be used to show interface statistics, including packets dropped because they were too large.

## Open vSwitch and Linux Bridges

In our deployment scenarios we use Open vSwitch (OVS, http://openswitch.org/) as the core mechanism for handling bridges. Many operators have reported struggling with quirks related to current versions of OVS. You will want to make yourself familiar with the basic OVS details. That means commands like `ovs-vsctl show` as well as those to help with debugging to look at flow control and other details, but that level of debugging is beyond the scope of what typical operators should need starting out.

> **Tip**
> If you are in a development environment, don't be afraid to restart the OVS daemon (using `sudo service openvswitch-switch restart`). Once you've confirmed your configuration is correct and the output of `ovs-vsctl show` is inconsistent with what you have configured and understand to be accurate about how the deployment should be working, then go ahead and restart the OVS daemon.
> 
> In production, this may still be the correct solution to certain OVS problems, but be aware that restarting this service will cause minor network service disruption. It may take anywhere from a few minutes to an hour to fully come back if you have a very large scale deployment. Long term, if you struggle with OVS in production, you may consider moving to a Linux Bridge model instead but that configuration is beyond the scope of this book.

Now, while we do specify OVS in our configurations, Linux Bridge is actually also used for iptables, which we'll discuss next, for your instances. If problems arise here, the bridge-utils package, which includes `brctl` to look into and manipulate bridges for instances, is installed on your compute node.

## Iptables

Another bit of debugging centers around another standard Linux tool—iptables (http://www.netfilter.org/projects/iptables/). Starting with the most basic of commands, you can run `sudo iptables -L` in order to get a listing of iptables rules. Just like the other commands, this can also be used in conjunction with the `ip netns exec` command to look at the router network run space, which, as you may recall, runs iptables for the instances. That means you could run something like the following on the controller node to get a listing of rules from both iptables:

```
$ sudo iptables -L
$ sudo ip netns exec qrouter-lc1c7574-9114-438f-aa33-1eb969a478f6a iptables -L
```

Since iptables is used for OpenStack's firewalls, doing a mere listing only scratches the surface of what iptables can do. The iptables command is used for adding and removing rules to do various types of traffic manipulation. If you find yourself needing to dig further into your install with iptables, use the online documentation for it or a reference book (e.g., Steve Suehring, 2015. Linux Firewalls. Upper Saddle River, NJ: Addison-Wesley) to dive deeper.

## Configuration Files

While building your own OpenStack deployment, you will find yourself looking at configuration files for services. In our sample deployments, Puppet creates these files, so you should not be editing them directly. However, understanding what you want Puppet to place in these files becomes important as you make decisions about your own deployment. If you do move on from Puppet entirely, or are doing a manual installation, you will be editing these configuration files by hand.

Most of the OpenStack config files are INI format files. The Puppet modules maintain the integrity of these files. If you are editing them manually, be sure to make a backup of the original file and then view and edit them with syntax highlighting for INI files enabled to help you spot problems. Some services, like Heat, also use templates that are in YAML, and you may even find some files in the OpenStack ecosystem that use JSON.

Whether your config file is INI, YAML, JSON or something else entirely, don't lose an afternoon to a missing or extra comma in a configuration file. Use a tool that highlights errors of these formats as effectively as possible. All modern text editors and software IDEs (integrated development environments) have support for these formats. There are also command line lint tools for YAML and JSON that can go into test jobs for configuration changes.

> **Tip**
> 
> All these formats allow a considerable amount of leeway. You probably will not find a perfect solution or one that you can fully automate to confirm the files are correctly formatted. The best they can do is help, especially for simple syntax errors.

## Puppet

We are using the official OpenStack Puppet modules in this book in order to craft our deployment scenarios, along with a deployments composition module that brings the pieces together specifically for this book. These have been tested and should work flawlessly. However, if you wish to make changes or find you're having problems, there are a few things you can do to figure out where your problem is. The first tool you have is running puppet apply with the --debug flag, for example:

```
sudo puppet apply --debug /etc/puppet/modules/deployments/manifests/role/foundations.pp
```
