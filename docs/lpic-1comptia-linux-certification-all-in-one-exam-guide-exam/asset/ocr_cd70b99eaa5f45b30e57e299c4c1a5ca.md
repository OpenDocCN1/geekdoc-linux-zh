The root user account is the superuser account for a Linux system. The root account can do anything it wants on the Linux system. The root user account is very powerful and must be used judiciously. Put bluntly, you can really make a mess of your system if you do something wrong. Because you're logged in as root, the system assumes you know what you're doing and will let you do it. For safety and security reasons, you should not use the root account for day-to-day work. Instead, you should create a standard user account for these tasks. When you actually need superuser privileges to complete a task, you can switch to the root user account. When the task is complete, you should switch back to your standard user account.

When you install Linux, you'll be prompted to provide a password for the root user account. You'll also be given the opportunity to create additional user accounts on the system. In your deployment plan, specify which user accounts you plan on creating. As with software packages, it's not a problem if you need to add or remove user accounts later on after the installation is complete. Linux provides an extensive set of tools to manage user accounts and passwords. I'll show you how to do this in a later chapter.

Once this information is in your plan, you're ready to move on to the next step: gathering network information. Let's review how this is done next.

# Gathering Network Information

In today's networked world, most of the Linux systems you will be working with will probably be connected to some type of computer network. Therefore, you need to gather the network information necessary for your system to connect to the network before you start the installation and include it in your deployment plan. Here's a list of questions you need to answer:

+   • Will the system have its networking configuration dynamically assigned, or will it need to be manually configured?

Most IP networks today use a Dynamic Host Configuration Protocol (DHCP) server to dynamically assign IP addresses and various other networking parameters to a workstation when it is booted on the network. Most Linux systems that will function as a desktop workstation will probably use this option. If this is the case, you don't need to do much to configure your networking parameters. The information will be dynamically assigned to the system every time it boots up.

However, if the Linux system is going to function as a server in the network, you shouldn't use DHCP to dynamically assign network configuration information. Using DHCP, the system could receive a different IP address each time it's booted. While this won't hurt a workstation, it can cause tons of problems with servers. Hence, network servers are usually assigned a static IP address that doesn't change.

If your system needs to have a static IP address assigned, then you need to gather the following parameters:

+   • IP address

+   • Subnet mask