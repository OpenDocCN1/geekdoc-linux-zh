EcoTOOLS has done specific integration work with the Tivoli and CA Unicenter management frameworks. The EcoTOOLS Plus Module for Tivoli TME 10 forwards events to the Tivoli Enterprise Console. Tivoli templates and filters are incorporated, which make it easier to run the EcoTOOLS GUI and distribute agent software from the Tivoli Enterprise Console. Similar integration has been done for CA Unicenter.

# Resource and Performance Monitoring Tools

This section describes tools for monitoring your application's overall performance and system resource utilization. It does not cover other areas, such as system call optimization for the application or code profiling.

Collecting application performance metrics is difficult, because defining the components making up the application is difficult. Some processes may be utility programs used by multiple applications. Even when the processes are known and are unique to an application, a performance tool may have difficulty mapping the use of shared resources, such as network buffers, to specific processes.

Different products have different ways of defining applications. For example, MeasureWare and PRM (Process Resource Manager) each have a different way of configuring applications. These methods are described briefly later in the chapter. PLATINUM's ServerVision also can monitor a group of processes as one application based on a user configuration. You must realize that you may need to reconcile the differences between the products' unique definitions to analyze application performance data properly.

# Application Resource Measurement

Because measuring the performance of an application is difficult, Hewlett-Packard and Tivoli Systems jointly developed an open set of APIs for measuring application response time. This standard set of APIs is called Application Resource Measurement (ARM). If applications are modified to use the new APIs at key points, end-users can then measure and control end-to-end performance of those applications. API calls are made in the application to mark the beginning and end of a transaction. A Software Developer's Kit (SDK) is freely available for ARM from either Tivoli or Hewlett-Packard to make this process easier. Only a few ARM APIs exist and they are listed in Table 7-1.

| Name | Function |
| :--- | :--- |
| arm_init | Initialize the ARM environment for the application |
| arm_getid | Name each transaction class used in the application |
| arm_start | Mark the start of execution of a transaction instance |
| arm_update | Update information about a transaction instance |
| arm_stop | Mark the end of a transaction |
| arm_end | Clean up the application's memory used by ARM |