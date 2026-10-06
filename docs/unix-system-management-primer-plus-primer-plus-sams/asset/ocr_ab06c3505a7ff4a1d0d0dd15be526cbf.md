# Chapter 7 • PATCHES, UPGRADES, AND DECOMMISSIONS 195

It's a good idea to keep the infrastructure from the old service up and running, or at least avail- to administrators, for a period of time after its decommission. With the old infrastructure on reserve, you can still retrieve data from or revert back to the original service if some- goes horribly wrong with the new service. When you've had ample time to determine that the old service is completely obsolete and supplanted by the new service, you can repur- the old infrastructure.

# Summary

Patches, upgrades, and decommissions are not very exciting parts of a system administrator's daily routine. Too often, system administrators ignore these basic system maintenance func- tions or perform them casually. As this chapter has explained, all changes to a Unix network require careful planning, testing, end-user execution, implementation, and follow-up support. To plan and implement a successful system upgrade or decommission, follow these general rules:

+   * Read all vendor documentation.
* Know who is using the services on your network.
* Test everything in a sandbox environment first. If you don't have a sandbox, lobby for one using the argument previously discussed.
* Notify users and management of upcoming changes.
* Back up your systems completely before doing anything!

# Review Questions

+   1. Why should a sandbox mimic your production environment?
2. Why is it advisable to patch an operating system in single-user mode? What steps you take before patching if you are unable to bring your system down to single-user mode?
3. What is a shared library and why is it an important part of an operating system upgrade?
4. How would you replace a disk in a server that does not support hot-swappable disks? What would be the procedure if the server did support hot-swappable disks?
5. What are three ways a system administrator can determine the end users of a particular service?