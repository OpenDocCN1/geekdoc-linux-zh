# Chapter 28 ◆ Emulation and Virtualization 719

consoles    Get information about domain consoles.

Commands on domains:

+   - balloon Set the domain's memory footprint using the balloon driver.
- create Create a domain.
- destroy Terminate a domain immediately.
- domid Convert a domain name to a domain id.
- domain Convert a domain id to a domain name.
- list List information about domains.
- max Set domain memory.
- migrate Migrate a domain to another machine.
- pause Execution of a domain.
- pingu Pin a domain to a cpu.
- restore Create a domain from a saved state.
- save Save state (and config) file.
- shutdown Shutdown a domain.
- synrq Send a syrq to a domain.
- unpause Unpause a paused domain.

Commands related to the xen host (node):

+   - dmesg Read or clear Xen's message buffer.
- info Get information about the xen host.
- log Print the xen log.

Commands controlling scheduling:

+   - atropos Set atropos parameters.
- bvt Set BVT scheduler parameters.
- bvt_ctxsalloc Set the BVT scheduler context allowance.
- robin Set round robin slice.

Commands related to virtual block devices:

+   - vbd-create Create a new virtual block device for a domain
- vbd-destroy Destroy a domain's virtual block device
- vbd-list List virtual block devices for a domain.

Commands related to virtual network interfaces:

+   - vif-list List virtual network interfaces for a domain.

Try '/usr/sbin/xenm help CMD for help on CMD