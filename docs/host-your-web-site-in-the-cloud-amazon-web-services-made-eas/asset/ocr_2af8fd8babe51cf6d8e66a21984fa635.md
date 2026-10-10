In the section called “Key Concepts” below, I’ll discuss the basic functions (for example, *RunInstances*) and the associated command line tools (ec2-run-instances). Keep in mind that the same functionality can be accessed using visual tools supplied by Amazon or by third parties, and that you can always build your own tools using the same APIs.

# Dollars and Cents

Because AWS is a pay-as-you-go web service, there’s a separate cost for the use of each service. You can model your AWS costs during development time to gain a better understanding of what it will cost to operate your site at scale. With sufficient attention to detail you should be able to compute the actual cost of serving a single web page, or performing some other action initiated by one of your users. You can also use the AWS Simple Monthly Calculator⁴ to estimate your costs.

With that in mind, let’s talk about pricing, metering, accounting, presentment, and billing before we look at the services themselves.

Pricing involves deciding what to charge for, how often to charge, and how much to charge. AWS charges for resource usage at a very granular level. Here are some of the pricing dimensions that AWS uses:

+   - Time—an hour of CPU time.
+   - Volume—a gigabyte of transferred data.
+   - Count—number of messages queued.
+   - Time and space—a gigabyte-month of data storage.

Most services have more than one pricing dimension. If you use an Amazon EC2 (Elastic Compute Cloud) server to do a web crawl, for example, you’ll be charged for the amount of time that the server is running and for the data that you fetch.

The web site detail page for each AWS service shows the cost of using the service. Each AWS service is published and visible to everyone. The pricing for many of the services reflects volume discounts based on usage; that is, the more you use the service, the less it costs per event. Pricing for the services tends to decline over time.