+   * Up to two additional query processes can be started if any resources remain after Level 2 needs are serviced.
+   * One additional query process can be started for each of the remaining levels if any resources remain from the previous level.

![](bbox=[0.15, 0.23, 0.9, 0.28])

Resource Manager can only manage the resources (i.e., CPUs) that are allocated to the instance by the server’s operating system. If other OS resource management tools are already managing the allocation of resources to Oracle at the OS level, then Resource Manager’s effectiveness may be limited.

The CPU and Parallel Query resource limits do not affect processing unless these resources are scarce at the system level. For example, if excess CPU resources exist on your server, then CPU resource management will have no effect. This would allow a process assigned little or no resources via a Plan Directive to be able to acquire as many CPU resources as it needs— even more than the amount specified in its assigned directive.