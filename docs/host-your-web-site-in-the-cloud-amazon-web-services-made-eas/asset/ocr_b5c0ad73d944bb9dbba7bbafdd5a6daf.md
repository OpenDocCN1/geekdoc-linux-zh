You can extend this program in various ways, such as combining it with the previous one and creating a user interface to allow the user to choose the dimension to be displayed. You might let the user close the date range using two copies of the jQuery Datepicker. $ ^{8} $ Also, you could embed this program into a larger monitoring or system control program. It can be as useful as you make it.

We've learned a lot in this section. We covered the fundamental concepts of CloudWatch, and saw how to enable Amazon CloudWatch for an EC2 instance and how to access the collected metrics. We also used the CloudFusion library to list the available CloudWatch metrics and to generate charts.

# # Learning and Using Apache JMeter

Let's take a short detour to learn more about a very useful program, the Apache JMeter.

# ## Why JMeter?

If you're running the charting program from the previous section and monitoring a nearly idle EC2 instance, you'll see little in the way of highs and lows. You can generate a system load manually by doing tasks such as:

+   * copying large files from place to place (generates disk read and write operations)
+   * downloading large files from the Internet (generates a load that's reflected in the Network In metric)
+   * placing large files on the server and downloading them externally (generates a load that's reflected in the Network Out metric)
+   * sorting very large files (increases CPU utilization, and disk read and disk write operations)

Unless you write some sophisticated test scripts, you'll quickly tire of doing this. Also, since generating a load is often the first step in a system optimization effort, you'll need to be able to reproduce the load with some degree of precision.

The Apache JMeter application simplifies the process of stress-testing a web-based application. Once a test plan has been created, it can be run at any time with a single click. The results are measured and stored for analysis.

^{8} http://docs.jquery.com/UI/Datepicker