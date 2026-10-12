![](bbox=[0.08, 0.05, 0.92, 0.55])

**Figure 4.1. The virtio RNG device**

Previously, Red Hat Enterprise Linux 7.0 and Red Hat Enterprise Linux 6 guests could make use of the entropy from hosts through the rngd user space daemon. Setting up the daemon was a manual step for each Red Hat Enterprise Linux installation. With Red Hat Enterprise Linux 7.1, the manual step has been eliminated, making the entire process seamless and automatic. The use of rngd is now not required and the guest kernel itself fetches entropy from the host when the available entropy falls below a specific threshold. The guest kernel is then in a position to make random numbers available to applications as soon as they request them.

The Red Hat Enterprise Linux installer, **Anaconda**, now provides the **virtio-rng** module in its installer image, making available host entropy during the Red Hat Enterprise Linux installation.

# 4.10. USING NETWORK-BOUND DISK ENCRYPTION

The Network-Bound Disk Encryption (NBDE) allows the user to encrypt root volumes of hard drives on physical and virtual machines without requiring to manually enter a password when systems are restarted.

In Red Hat Enterprise Linux 7, NBDE is implemented through the following components and technologies: