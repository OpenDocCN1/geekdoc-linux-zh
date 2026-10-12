
- **Look for performance data from customer sources** This is where the user and/or the tester have their opportunity to give you feedback on how the tests went. This might also be where the application testers can offer helpful information.

Once you have completed the analysis phase, you are ready to start forming a hypothesis on what the problem might be and how to solve that problem.

## Step 4: Create a Hypothesis

The goal of this phase is to develop a theory or hypothesis on what is causing the performance problem. Creating a hypothesis could be very simple or quite complex. In the case of multiple problems, you might just be creating a hypothesis for one or two problems. Remember, you don’t have to solve all of the problems in one shot; in fact, you are better off changing only a few, or one thing at a time. The tasks involved include the following:

- **Determine if there actually is a problem** Sometimes you come to the conclusion that the system is running as designed, and there really isn’t a problem. This could be the hypothesis that you come up with.

- **Formulate a theory** Formulating a theory is the most important part of the tuning art. Here, you have to take in all of the data that you have gotten and try to determine why you are having the problem, if there actually is a problem. The types of problems that you might theorize include I/O problems, locking problems, poorly formulated SQL statements, etc.

- **Back that theory up with data** A theory with no supporting data isn’t worth very much. Even if the data isn’t conclusive, there should be some indications from the data to support your theory.

The hypothesis is essential for proposing solutions. If you can’t determine what you think the problem is from the data that you have gathered, you need to go back and gather data that is more useful.

## Step 5: Propose a Solution

The goal of this phase is to come up with a proposed solution or a test in order to determine what the actual solution should be. In some cases, the solution might be to purchase more hardware, such as disk drives or memory. In other cases, the solution might be to tune some SQL statements or add an index. This phase is where you get to actually propose the tuning solution, which needs to consist of these tasks:

- **Develop a solution** This solution could involve adding indexes, changing SQL statements, changing the hardware layout, or adding more hardware.

- **Develop a validation plan** The validation plan should include some procedures that can validate that the change has been made correctly.

- **Document expected results** It is easier to run a test when you have some expectations of what the results should be. This allows you to determine if the test might be flawed in some way. If you don't get the expected results, either the test is flawed or the solution is flawed.

When proposing a solution, you should always have the result of that solution in mind. If you don't know what the proposed solution is going to do, then why do it?

## Step 6: Implementation of Solution

This step is really fun part. The goal of this phase is to actually fix the performance problem. Here is where you get to make the changes that you have proposed and get ready to test the solution in order to validate your hypothesis. Implementing the solution could be as easy as adding an index, or as difficult as changing out the entire storage subsystem. In any case, this is where the action takes place and can involve some of the following tasks:

- **Make the hardware change** This might involve upgrading hardware, changing the I/O subsystem, or replacing the entire system and migrating to a new system.

- **Make the configuration parameter change** This is usually pretty easy and doesn't involve too much risk.

- **Add an index** Adding indexes can be quite time-consuming on large tables. The time it takes depends on the data and the complexity of the index.

It is important when making changes to follow a few simple rules. These rules will make your job easier and give you better results in the end:

- **Document your changes** By documenting your changes, you will be better able to reproduce them and be able to determine which changes helped.

- **Only change one thing at a time** Multiple changes at a time lead to unpredictable results.

- **Document your changes** This is in the list twice because it is so important.

By being methodical and careful, you can achieve great results.

## Step 7: Test and Monitor

This phase involves running validation and performance tests against the changed system. The goal of this step is to validate the solution that you have executed in the previous step. This validation involves confirming that the change made an improvement, that the change made things worse, or in some cases, that the test is flawed.

- **If possible, test the change in a nonproduction environment.** This requirement is sometimes impossible, but it should be a goal of all tuning. In any case, the risk of the change should be evaluated and a determination of how to test and implement the change should be made. For example, adding or changing an index could affect performance, but not the resulting data returned by a query. A change to a query itself could return incorrect results.

- **QA the change before deploying.** Any code change should have quality assurance tests performed on it before it is deployed.

- **If possible, run load tests.** Load tests can help you to measure and document the performance gain from the change. The better the test, the better the results. A third-party I/O stress tool can be used, such as Loadrunner, iozone, postmark, or ORION.

- **Monitor the changes using the monitoring tools described in step 2.** If you use the same tools and monitor in a similar fashion, you can compare the results with those collected in step 2.

- **Document the changes.** If you don't document what you did, it might be very difficult to reproduce the change and to determine how it affected performance.

It is important that changes be made carefully and methodically. Too many changes at one time can lead to unpredictable results.

## Further Analysis and Testing

You should now pick up with step 3 and repeat until you are satisfied with the results of your tuning, or you are out of time or budget. Unfortunately, tuning is like cutting grass; it always grows back. The end point of tuning is when one of several events occur:

- **The performance goals have been met** This could be a certain average response time, batch jobs running within a specific time window, etc.

- **The time has expired** Sometimes you only have test equipment for a limited time frame and you must end testing when that time frame has been met.

- **The budget has been used up** Many performance tuning exercises have a specific budget, and once those funds have been used up, tuning must stop.

These and many other reasons could dictate the end of the tuning engagement. Hopefully, once you are done, the results are better performance or a recommendation on how to improve performance.

But how do you actually tune the system? That is the subject of the remainder of the chapter. This will start with monitoring and tuning the Oracle instance.

## Tuning Oracle on Linux

Tuning Oracle on Linux, or on any platform for that matter, can be broken down into three major areas: application tuning, instance/database tuning, and hardware tuning. These different tuning areas can be attacked in any order, but typically application tuning is tackled first, then instance and database tuning, and then hardware tuning. However, a general survey of the entire system should be performed first, and then a determination made of which area deserves the most immediate attention. Each of these areas of focus can be quite involved but might lead to the solution to the root cause of your performance problems.

- **Application tuning** This involves modification of application code, SQL statements, and processes that might be inefficient or a bottleneck. Application tuning also includes stored procedures and modification of the database schema, including index tuning.

- **Instance/database tuning** Instance tuning involves the modification of Oracle initialization parameters to change the configuration of the Oracle instance. Instance tuning might also involve the need to modify Linux parameters.

- **Hardware tuning** Hardware tuning involves the modification, reconfiguration, and addition of hardware in order to improve Oracle performance.

Tuning only one of these areas will not provide a complete performance evaluation and improvement. Tuning the Oracle instance when the application code is a problem will not be effective. Similarly, tuning the application and Oracle instance when you have an I/O problem can also be ineffective. A complete performance evaluation and tuning exercise needs application, instance, database, and hardware tuning.
