![](bbox=[0.15, 0.06, 0.42, 0.35])

hus far, you have examined tuning techniques for two SGA components: the Shared Pool and the Database Buffer Cache. These two SGA components, and the Redo Log Buffer discussed in Chapter 7, “Tuning Redo Mechanisms”, are used by every Oracle application. This chapter, however, will focus on tuning three areas within the SGA that may or may not be utilized in all environments:

+   - Shared Pool architectural components
+   - Large Pool
+   - Java Pool

Because some Oracle environments do not make use of these SGA components, this chapter will discuss the essential concepts related to each of these areas before introducing the techniques used to monitor and enhance their performance.

# ## Shared Server Concepts

Each Oracle application user has two processes associated with their connection to the database: a User Process, which executes on the user’s client machine or on the application’s web server, and a Server Process, which executes on the Oracle Server machine.

In the default Oracle9i configuration, called Dedicated Server, each user’s Server Process is dedicated to servicing requests for that user’s session only. On Unix systems these Server Processes execute on the Oracle server as individual OS processes. If there are 50 connected users, then there will be 50 corresponding Server Processes running on the Oracle server machine to service their database activities.

A second optional configuration, called Shared Server, is also available. In this configuration, several Shared Server processes are created on the Oracle