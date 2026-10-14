space. Rollbacks are useful if you are experimenting with a Linux system and are concerned that updates might interrupt your work.

Finally, in the Package Exceptions tab (see Figure 10-7), you can identify packages or files that you don’t want to have automatically updated by Red Hat Network. By default, the list includes only packages beginning with “kernel,” with the assumption that you don’t want your kernel upgraded without making that decision yourself. You can add other packages or even individual files based on which services you consider critical or don’t want to have altered without explicit action on your part.

![](bbox=[0.18, 0.37, 0.78, 0.78])

# Figure 10-7 The Package Exceptions tab of the Red Hat Network Configuration tool

When you click OK in this configuration window, you are taken to the Red Hat Network update windows, where the server is contacted and upgrades to packages installed on your system are identified and downloaded.

The basic Red Hat Network service described here is part of a larger Red Hat Network architecture that Red Hat Software provides at an extra cost to customers who purchase Red Hat Enterprise Linux products. In addition to the basic service, Red Hat Software highlights the Management and Provisioning products within Red Hat Network’s offering.

By purchasing access to these services, you can add capabilities such as those in the following list to help keep your systems secure and up to date. The great advantage in these pay services is the ability to work with multiple Linux servers through a single interface, rather than trying to log in to multiple systems, collect data about what is installed or needing upgrading, and then coordinating it from a central location. Red Hat Network automates all of these functions: