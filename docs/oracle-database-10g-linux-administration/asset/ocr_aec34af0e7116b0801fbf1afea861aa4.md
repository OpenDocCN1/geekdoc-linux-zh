the number of users, you reduce the software cost. In addition, you might be able to reduce the number of load-driving systems that are necessary in order to produce the required load.

# ## Database Testing Only with Full Application Emulation

You can test the database layer through the application by modifying the application layer to simulate database requests. This involves some modification of the application in order to create this load. With this type of testing, you can simulate the user load on the database system and capture response times without having to incur the cost of load-generating systems. This type of testing works only if you have built this type of feature into your application.

The data collected will allow you to determine database response times and information about the database calls such as execution plans, data access patterns, and instance performance information, but doesn’t tell you much about additional latencies introduced at the application server layer. However, if the database layer is the problem, this type of testing can be useful.

# ## Database Testing Only with No Application Emulation

With this type of testing, the application is taken out of the picture. SQL statements can be captured from users running against the application, and a load test can be developed that simulates these types of SQL statements without running any application code. This is not the best type of test, since the application layer is completely removed, but it is better than no load testing at all.

This type of test can sometimes be developed in a few weeks in C code, Perl, or shell scripts, and it can be deployed quickly. This type of test cannot provide sizing information, but it is great for putting a system under load in order to validate new hardware components and system settings. It is also a great way to stress the database instance.

This is by far the most economical load test, since it can often be developed in-house. As the testing evolves, so can the test itself. I often use this type of test in my performance tuning classes in order to simulate some load on the system quickly and easily.

# # Performance Metrics

When doing any kind of load testing, it is important to determine the performance metrics before the testing begins. Don’t focus on one single metric, but use many metrics. There are a number of great metrics that you can use. Here is a list of some of them:

+   -   OS Metrics
+   -   **CPU** CPU utilization is one of the best metrics, since you can only use 100 percent of the CPU time. This should be broken down into system CPU time, user time, and kernel time.