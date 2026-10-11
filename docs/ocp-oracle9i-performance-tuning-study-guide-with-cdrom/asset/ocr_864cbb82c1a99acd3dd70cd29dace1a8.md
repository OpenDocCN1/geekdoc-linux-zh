these same resources. Any database tuning effort should also include an examination of these OS resources so that changes made to improve database performance do not cause OS-related problems like OS paging and swapping, or excessive CPU consumption.

Oracle Resource Manager is used to allocate CPU and Parallel Query resources to users. The resource plan directives are where the actual CPU and degree-of-parallelism allocations are defined using the DBMS_RESOURCE_MANAGER PL/SQL package. Once directives are defined, they are assigned to resource plans, which are assigned to resource consumer groups, which are in turn assigned to database users or roles. The resource plan for the instance can be defined using the RESOURCE_MANAGER_PLAN parameter in the init. ora or by issuing the ALTER SYSTEM SET RESOURCE_MANAGER_PLAN command. Several data dictionary and dynamic performance views are available to monitor and manage the resource consumer groups, resource plans, and resource plan directives.

# ## Exam Essentials

+   - **Understand the OS tuning process.** Be able to describe the order in which the components of OS tuning should be examined. Also be able to explain how to measure the current performance of those components using operating system commands and utilities.

+   - **Know how paging and swapping differ.** Understand when paging and swapping occurs, how to detect it when it happens, and where paged or swapped objects are stored. Be able to describe what steps can be taken to minimize paging and swapping.

+   - **Understand the role of Resource Manager.** Be able to explain all the steps required to implement Resource Manager. Know what privileges users must be granted in order to perform Resource Manager operations. Understand which data dictionary and dynamic performance views can be used to monitor Resource Manager and the contents of each.