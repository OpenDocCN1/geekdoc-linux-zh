# Chapter 14 INTERNAL COMMUNICATION

**Relational naming conventions assign related names to related machines.** These naming schemes aren't terribly practical, theyre common—especially in internal networks. At the University of Michigan, the public login server pool was named after classic video games, lab workstations were named after types of bread, and mail servers were named after monsters from old Japanese movies (Godzilla, Mothra, and so). In addition to their entertainment value, relational names are easy to remember and communicate. It is much easier to say "Log in to pacman" than it is to say "Log in aa-login12".

![](bbox=[0.105, 0.252, 0.163, 0.298])

# Dual Names

Some organizations use DNS tricks to provide relational naming internally while providing the public with more appropriate functional or geographic names.

# Summary

This chapter has introduced several effective mechanisms by which a system administrator can communicate with him or her coworkers. Writing documentation—including procedures, diagrams, and host lists—is the first step in establishing communication. Change management is the next step; this process implements approval, notification, and auditing for all changes on your systems, help stabilize your systems and minimize the number of surprises that result from unannounced changes. Finally, revision control is used by system administrators to track changes to configuration files. The most popular revision control tool is RCS, which is available on all Unix systems.

System administrators are not traditionally known as effective communicators, but it is a required skill that becomes more important as you move up in your organization. Administrators who can properly document their procedures, interact with other departments to communicate changes, and maintain control of their own infrastructure will find themselves in much better standing in their own department as well as in other areas within their organization.

# Review Questions

+   1. What is the difference between a physical and a logical network diagram?
2. What makes the following step in an operating system installation procedure incomplete?

Log in to the Jumpstart boot server and add your new machine to Jumpstart's configuration.