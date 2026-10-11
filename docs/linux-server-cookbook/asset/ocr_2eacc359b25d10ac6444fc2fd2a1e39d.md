Some important principles when IT automation is used are as follows:

+   * **Make it simple**: Automation tasks should solve a specific need and not a general one. Complex automation tasks lead to less flexibility and a higher probability of needing human intervention.
+   * **Idempotent**: Ensures if one system is already configured, running the same automation process will not cause any modification and downtime to the system.
+   * **Imperative versus declarative**: Imperative model focuses on performing tasks to obtain the desired result, and on the other hand, the declarative model defines the desired state. For example:
+   	* **Imperative model**: Running a command to create a virtual machine with specific options.
+   	* **Declarative model**: Using an automation tool that reads the desired virtual machine definition and the state of the same. It ensures that it exists and that the state is desired. Otherwise, it will perform the needed actions to obtain the expected definition.
+   * **Mutable versus immutable**: Traditional infrastructures were more mutable after creation than modern ones. Updating operating system, libraries, and applications were a common task for system administrators. Modern systems, especially using virtual machines and containers, are more likely to be destroyed and deployed with the new versions of the distribution or the application running on it. Modern infrastructures are considered as immutable infrastructures.
+   * **Do not repeat yourself**: One of the most important principles is to be able to reuse part of the automation definitions. Automation tools allow to create reusable part of codes and use it on different projects.

Inside the IT infrastructure are different categories depending on the purpose of the tasks to perform. Automation evolved over the years from simple local tasks through multiple managed systems to reach the current status, which includes the following:

+   * **Configuration management**: This automation ensures the managed devices have the proper configuration and applies the modification