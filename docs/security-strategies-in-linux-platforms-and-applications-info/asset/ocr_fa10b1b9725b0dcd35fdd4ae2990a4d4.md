# CHAPTER 11 | Managing Security Alerts and Updates

Sometimes, you'll need to get into the details of associated bug reports. To that end, Ubuntu maintains its Launchpad system and Red Hat has a Bugzilla system for classifying and tracking bugs. Different user and service applications maintain their own systems. If you know how to navigate through these systems, you'll have a better idea whether key developers are taking the problems you see seriously. If you've done the research, don't hesitate to report a bug. If it is a security issue, some developers ask for private reports.

In the open source world, organizations like ISECOM, the NSA, and even the FSF are working toward improving security on open source software. If you've identified a problem, be aware of the open source culture before reporting it. If you do a little research, you may get the attention of prominent Linux developers and a faster solution.

There are several ways to create a local update repository. The simplest reason is to reduce the load on the network's Internet connection. Other reasons include limiting software available to local systems. In addition, a local update repository allows you to test updates before they're installed on local systems.

If you just need to reduce the load on an Internet connection, solutions such as the Red Hat Satellite Server and the Red Hat Proxy Server are available. If you need to administer a substantial number of systems, centralized system management tools such as the Red Hat Network, Canonical's Landscape, and Novell's Zen Linux Management tools can be helpful. Alternatively, if you prefer open source centralized management solutions, monitor the work of Red Hat's Spacewalk project.

# CHAPTER SUMMARY

This chapter describes what you can do with security alerts and updates. Security alerts are provided not only by the developers behind Linux distributions but also by the developers behind major Linux applications from the OpenOffice.org suite to the Apache Web server. The apt-* and yum commands are two ways to install these updates; packages that automatically download and install packages are also available.

+   Alternatively, if you administer a variety of Linux computers, system management solutions such as the Red Hat Network and Canonical's Landscape can help you manage groups of systems. They can help you monitor the status of such systems, pushing different sets of updates to these systems as desired.