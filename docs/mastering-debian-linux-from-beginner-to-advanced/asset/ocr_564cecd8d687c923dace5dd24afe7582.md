+   - **User-friendly**: Intuitive graphical user interface for easy VM management.
+   - **Snapshot functionality**: Create and restore VM snapshots for easy rollback.
+   - **Shared folders**: Easy file sharing between host and guest systems.
+   - **USB device support**: Connect USB devices directly to virtual machines.

# How VirtualBox Works:

+   1. VirtualBox installs on the host operating system.
+   2. It creates and manages virtual machines, each with its own virtual hardware.
+   3. The VirtualBox hypervisor mediates between the guest OS and the host's physical hardware.
+   4. Guest additions can be installed to improve performance and enable additional features.

# Comparing KVM and VirtualBox

| Feature | KVM | VirtualBox |
| :--- | :--- | :--- |
| Type | Type 1 (Bare-metal) | Type 2 (Hosted) |
| Performance | Near-native | Good, but may have some overhead |
| Host OS | Linux only | Cross-platform |
| Management | Command-line focused (with GUI tools available) | GUI-focused |