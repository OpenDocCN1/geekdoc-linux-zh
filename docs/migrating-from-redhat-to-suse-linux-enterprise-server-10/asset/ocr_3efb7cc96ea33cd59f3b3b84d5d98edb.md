+   * **domid**. A numeric, consecutive domain ID, which is automatically assigned when the domain starts.
+   * **memory**. The amount of memory assigned to the domain.
+   * **vcpus**. The number of virtual CPUs utilized by this domain.
+   * **state**. The current state of the domain. This could be:
+       * **r**. The domain is running.
+       * **b**. The domain has been created, but is currently blocked. This can happen, when a domain is waiting for I/O or when there is nothing to do for the domain.
+       * **p**. The domain is paused. The state of the domain is saved and can be restored.
+       * **s**. The domain is in the process of being shutdown.
+       * **c**. The domain is crashed, due to an error or misconfiguration.

An alternative to list is the command **top**, which displays domain information updated in real-time.

The **console** command connects you with the terminal of a running domain:

```
xm console <domain_id>
```

The command takes the domain id as a parameter, which can be determined with the **list** command (field domid). As mentioned before, use the key combination **Ctrl-J** to disconnect from a terminal.

With the **pause** command you can interrupt the execution of a domain temporarily:

```
xm pause <domain_id>
```