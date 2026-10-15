In Figure 7-5, the CPU information is not correctly displayed. The System z hardware does not support the CPU performance counters required by OProfile yet, however the output does contain valuable information.

```
CPU: CPU with timer interrupt, speed 0 MHz (estimated)
Profiling through timer interrupt
vma      samples   %     app name          symbol name
80002840 5862     34.8970 mcf_base.z_Linux  price_out_impl
800012c8 5221     31.0811 mcf_base.z_Linux  refresh_potential
800003c4 4398     26.1817 mcf_base.z_Linux  primal_bea_mpp
80003b60 408      2.4289 mcf_base.z_Linux  sort_basket
0001a67c 345      2.0538 vmlinux            default_idle
800013d8 138      0.8215 mcf_base.z_Linux  flow_cost
800003bc 98       0.5834 mcf_base.z_Linux  update_tree
800020f8 88       0.5239 mcf_base.z_Linux  dual_feasible
800036a4 72       0.4286 mcf_base.z_Linux  primal_minus
8000323c 40       0.2381 mcf_base.z_Linux  write_circulations
80002720 24       0.1429 mcf_base.z_Linux  insert_new_arc
```

Figure 7-5 OProfile output

The output includes:

+   vma	The virtual memory area (vma) is a contiguous area of virtual address space. These areas are created during the life of the process when the program attempts to memory-map a file, links to a shared memory segment, or allocates heap space.
+   samples	The number of samples for the symbol
+   %	The percentage of samples for this symbol relative to the overall samples for the executable
+   app name	The application name to which the symbol belongs
+   symbol name	The name of the symbol that was executed

From the report of OProfile, we can analyze the performance of a target module and adjust tuning accordingly. For example, in Figure 7-5, modules of the application mcf_base.z_Linux consume most of the CPU time. To improve the performance of this application, more attention should be paid to these modules than the others.

> Note: For details and documentation about the OProfile commands, see: http://oprofile.sourceforge.net/docs/