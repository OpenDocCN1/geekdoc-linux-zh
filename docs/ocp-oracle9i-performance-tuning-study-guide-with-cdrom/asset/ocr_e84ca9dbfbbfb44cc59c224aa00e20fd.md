typically gathered by running Oracle-supplied scripts, monitoring activity through the use of a GUI tool, or by examining database trace and log files. The resulting statistics are frequently expressed in terms of ratios, percentages, or wait times. Other statistics are expressed in terms of throughput. *Throughput* is the amount of processing that a computer or system can perform in a given amount of time. An example of throughput might be, “How many customer deposits can we post to the appropriate accounts in four hours under regular workloads?” Throughput is an important measure when considering the scalability of the system. *Scalability* refers to the degree to which additional users can be added to the system without having system performance decline significantly. New features like Real Application Clusters make Oracle9i one of the most scalable database platforms on the market.

![](bbox=[0.14, 0.41, 0.2, 0.44])

> Performance tuning considerations for Online Transaction Processing Systems usually revolve around throughput maximization.

# Timings

Timings related to performance tuning are usually related to response times. *Response time* is the amount of time it takes for a single user’s request to return the desired result while using an application. An example of response time might be “How long does it take for the system to return a listing of all the customers who have purchased products that require service contracts?” Another example of tuning-related timings is time that users are spending waiting for access to a particular database resource.

![](bbox=[0.14, 0.71, 0.2, 0.74])

> Performance tuning considerations for Decision Support Systems usually revolve around response time minimization.

# Setting Performance Goals

Once you have established a good baseline against which you’ll measure your tuning activities, you need to establish measurable tuning goals. These goals should be specific and stated in a measurable way that allows you to use your existing data for comparison.