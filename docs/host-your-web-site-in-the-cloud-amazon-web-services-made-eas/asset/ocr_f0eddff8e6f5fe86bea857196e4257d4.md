create an RDS DB Instance with a single web service call. The instance will be up and running and ready for use within a few minutes.

After you finish reading this chapter, I think you’ll agree that Amazon RDS can actually change the way you think about a relational database. You can create, use, terminate, and restore your DB Instances on an as-needed basis.

Perhaps you’re moving an application to the cloud and each installation of the application requires a private MySQL database. You can automate the entire installation and provisioning process. Each time a new customer signs up for your service, your code can call the RDS CreateDBInstance API operation to create a new DB Instance.

Maybe you have a multi-tier application and you want to set up a fully automated test environment. Again, using the Amazon RDS APIs (or the command line tools), you can create, use, and terminate DB Instances as part of your testing process.

Or, consider this: say your application accumulates data slowly but consistently throughout the month, and provides access to the data through some simple, low-overhead queries. At the end of each month, however, your application initiates a day-long billing run, during which the queries become complex and time-consuming. Using Amazon RDS, you can host the database on a system of moderate power for 95% of the month, scale up once per month to support the billing run, and then scale back down afterwards. You could do this on a daily, weekly, or even seasonal basis as your needs change. You can also add extra storage space to your database as your needs grow.

Sound interesting? Let’s learn more!

# MySQL Code Ahead

![](bbox=[0.09, 0.69, 0.13, 0.72])

This chapter assumes that you have some basic familiarity with MySQL. If you know how to use the mysql command from the command line, you’re in good shape. Of course, you’ll need to have MySQL installed on your system; chances are you’re already good to go, as you’ve likely installed it along with PHP. If that’s not the case, Chapter 1 of Kevin Yank’s Build Your Own Database Driven Web Site Using PHP and MySQL is freely available on sitepoint.com, ${}^{1}$ and contains detailed installation instructions for every platform.