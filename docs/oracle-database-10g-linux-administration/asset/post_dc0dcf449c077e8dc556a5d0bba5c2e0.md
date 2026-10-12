
Assumption may or may not be correct. Remember that two disk drives perform better than one disk drive. One of the most common performance problems that I run into is when the customer replaces four 18GB disk drives with one 72GB disk drive (or something similar). I would automatically expect this system to perform more slowly than the original.

Load-testing the same application on two different hardware platforms provides an excellent comparison. Keep in mind that this test will provide useful data only if the application is not the problem. You must keep this in mind because you might actually be experiencing a performance improvement that you don’t realize, because that improvement is masked by other factors. The result of any performance test always has three possible outcomes:

- **Performance has improved** This is pretty easy to measure and determine.
- **Performance has gotten worse** This is also fairly easy to measure and determine.
- **The test is flawed or there are outside factors affecting the test** For example, if you believe you have an I/O problem and you add I/O performance capacity and see no improvement, it might be that you really don’t have an I/O problem at all, or that the load test itself is not driving enough load to show the improvement. This is why proper metrics are important.

With this type of comparison, you can often collect a lot of excellent data. It is important that it be analyzed and interpreted correctly.

## New Hardware and a New Application
This is probably the most difficult type of data to interpret. With a new application and new hardware, you can still collect baseline performance data, analyze execution plans and data access patterns, and develop metrics that you will use in the future. With this type of test, it is still important to perform load testing and, if possible, compare the results against service-level agreement (SLA) metrics. This is your opportunity to determine if the new application and hardware will meet your needs before introducing them to the user community.

## Load-Testing Batch Jobs
Load-testing batch jobs is fairly easy relative to load-testing OLTP applications. This is due to the fact that batch jobs are not run interactively and the queuing and execution of batch jobs is usually controlled by the application or by the DBA staff. Because of this, it is a relatively straightforward task to run the batch jobs, monitor performance of Oracle and the OS while these jobs are running, and document batch performance.

Most batch processing systems log the performance of each batch job run, including information such as

- Start time
- End time
- Duration
- Job parameters
- User information

Because you have this information, you can run the same batch job on the test system and compare the run time on the current system with that on the test system. Keep in mind that unless you are moving to a new hardware platform, this data will provide baseline performance data only.

### Load-Testing Loading
As with batch jobs, load-testing database loading is fairly easy relative to load-testing OLTP applications. Loading data into the database is done in an offline fashion, usually when there is not a lot of other activity on the system, and it is almost always timed. When setting up performance metrics on loading, try to collect at least the following data:

- Start time
- End time
- Duration
- Job parameters
- Number of rows being loaded
- Amount of data (size) being loaded

If this information is stored in a database table, you can easily track trends and potential issues before they become problems. From this data, of particular interest is the amount of data being loaded vs. the duration. Any significant slowdowns should alert the DBA staff.

### Load-Testing OLTP Applications
Load testing of OLTP applications is the most difficult, since OLTP systems are characterized by

- Many online users
- Multiple applications performing different functions
- Random data access patterns
- Continuous activity
- Peak and low utilization periods

In order to properly load-test OLTP applications, you must simulate many users simultaneously accessing the system. This simulation can take several forms and can work in several different ways. The following list represents different types of load tests that can be done with different levels of cost and quality of data.

- Full end-to-end testing with 100%+ users
- Full end-to-end testing with partial users
- Database testing only with full application emulation
- Database testing only with partial application emulation

The value of the load testing diminishes as you go down the list, but then so does the cost. Although the load-testing software available today is very good, it is also very expensive. It is priced beyond the reach of many budgets. Minimal load testing is still much better than no load testing at all.

## Full End-to-End Testing with 100%+ Users
In this type of test, load-testing software emulates the user load against the full application environment. This means that HTML is emulated and is requesting data from the application, which in turn requests this data from the database. If possible, the number of users that you expect to support should be emulated, and then ramped up until the system cannot support any more load. This point will be your maximum capacity. In full end-to-end load testing, components such as keyboard time and think time are factored into the test.

The TPC-C benchmark is a perfect example of where a full end-to-end test is done. This type of test actually simulates all of the users that might be connected to this type of system, and runs a complete application. The system being tested includes web servers, the application, and the database itself.

## Full End-to-End Testing with Partial Users
This type of test can also be effective. With a partial user test, you would most likely remove the think time and key time from the simulation, and blast the system with requests as quickly as possible. The data is useful, since it can point out flaws in the application or database. However, the user count information is not as valuable.
The reason to perform partial user testing is to reduce the amount of hardware and software necessary in order to create the user load. Many of the commercial load-testing software packages, such as Loadrunner and Silk Performer, are licensed according to the number of simulated users that you will be emulating. By reducing
the number of users, you reduce the software cost. In addition, you might be able to reduce the number of load-driving systems that are necessary in order to produce the required load.

### Database Testing Only with Full Application Emulation
You can test the database layer through the application by modifying the application layer to simulate database requests. This involves some modification of the application in order to create this load. With this type of testing, you can simulate the user load on the database system and capture response times without having to incur the cost of load-generating systems. This type of testing works only if you have built this type of feature into your application.

The data collected will allow you to determine database response times and information about the database calls such as execution plans, data access patterns, and instance performance information, but doesn’t tell you much about additional latencies introduced at the application server layer. However, if the database layer is the problem, this type of testing can be useful.

### Database Testing Only with No Application Emulation
With this type of testing, the application is taken out of the picture. SQL statements can be captured from users running against the application, and a load test can be developed that simulates these types of SQL statements without running any application code. This is not the best type of test, since the application layer is completely removed, but it is better than no load testing at all.

This type of test can sometimes be developed in a few weeks in C code, Perl, or shell scripts, and it can be deployed quickly. This type of test cannot provide sizing information, but it is great for putting a system under load in order to validate new hardware components and system settings. It is also a great way to stress the database instance.

This is by far the most economical load test, since it can often be developed in-house. As the testing evolves, so can the test itself. I often use this type of test in my performance tuning classes in order to simulate some load on the system quickly and easily.

## Performance Metrics
When doing any kind of load testing, it is important to determine the performance metrics before the testing begins. Don’t focus on one single metric, but use many metrics. There are a number of great metrics that you can use. Here is a list of some of them:

- OS Metrics
- **CPU** CPU utilization is one of the best metrics, since you can only use 100 percent of the CPU time. This should be broken down into system CPU time, user time, and kernel time.
