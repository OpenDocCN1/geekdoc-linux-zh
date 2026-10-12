**Description:** Reference index for each monitored system process. Because the *procTable* is in fact a table, the *prIndex* **is used** to access another instance of the table

+   * **Object Name:** *prNames*
+   * **OID:** *prEntry.2*
+   * **Object Type:** Display String [255]
+   * **Access Mode:** read-only
+   * **Description:** The name of the process that the agent is monitoring. The process name is obtained from the agent configuration file after the *proc* keyword command

+   * **Object Name:** *prMin*
+   * **OID:** *prEntry.3*
+   * **Object Type:** Integer
+   * **Access Mode:** read-only
+   * **Description:** The minimum number of processes that should be running on the system. If the number of processes is less than the minimum, an error flag is generated in the *prErrorFlag* and *prErr-Message* MIB objects. The minimum value is obtained from the agent configuration after the maximum value, if any, has been specified

+   * **Object Name:** *prMax*
+   * **OID:** *prEntry.4*
+   * **Object Type:** Integer