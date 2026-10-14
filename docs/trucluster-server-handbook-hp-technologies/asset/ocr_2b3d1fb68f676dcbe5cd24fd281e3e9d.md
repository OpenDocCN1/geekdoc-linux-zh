# 23.4.17.1 Command-Initiated

There are three commands that cause CAA to evaluate the placement and balance of application resources:

+   - The caa_balance command.
+   - The caa_start command (covered in section 23.4.14).
+   - The caa_relocate command (covered in section 23.4.16).

Starting in V5.1B, the caa_balance command can be used at any time to reevaluate the placement of application resources within the cluster.

+   - Reevaluate all application resources in the cluster.
+   ```
+   # caa_balance -all
+   Attempting to stop `cluster_lockd` on member `alph11`
+   Stop of `cluster_lockd` on member `alph11` succeeded.
+   Attempting to start `cluster_lockd` on member `alph12`
+   Start of `cluster_lockd` on member `alph12` succeeded.
+   Resource clustercron is already well placed
+   Resource memberUP is already well placed
+   clustercron is placed optimally. No relocation is needed.
+   memberUP is placed optimally. No relocation is needed.
+   powerUP is placed optimally. No relocation is needed.
+   ```

+   - Reevaluate the resources on a particular cluster member.
+   ```
+   # caa_balance -s molari
+   Attempting to stop `cluster_lockd` on member `alph13`
+   Stop of `cluster_lockd` on member `alph12` succeeded.
+   Attempting to start `cluster_lockd` on member `alph11`
+   Start of `cluster_lockd` on member `alph11` succeeded.
+   Resource memberUP is already well placed
+   Resource powerUP is already well placed
+   memberUP is placed optimally. No relocation is needed.
+   powerUP is placed optimally. No relocation is needed.
+   ```

+   - Reevaluate specific application resources.
+   ```
+   # caa_balance memberUP powerUP
+   Resource memberUP is already well placed
+   Attempting to stop `powerUP` on member `alph11`
+   Stop of `powerUP` on member `alph11` succeeded.
+   Attempting to start `powerUP` on member `alph12`
+   Start of `powerUP` on member `alph12` succeeded.
+   memberUP is placed optimally. No relocation is needed.
+   ```

For more information on application resource load-balancing, see the caa_balance(8) reference page as well as the TruCluster Server Cluster Highly Available Applications guide.