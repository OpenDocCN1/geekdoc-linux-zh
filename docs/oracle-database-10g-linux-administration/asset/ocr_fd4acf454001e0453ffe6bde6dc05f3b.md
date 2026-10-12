Loading Loading data into the database can be simulated in a test environment using the production data.

OLTP Here is where it gets interesting. It is desirable to simulate the entire application environment (i.e., web servers, application tier, database layer) if at all possible, with as many simulated users as you can.

Let’s look at the first question and then some of these environments in a little more detail.

# ## Why Is the System Being Tested?

There are a few basic goals in load testing. These goals vary, depending on what is changing. Load testing can be used to validate the performance impact of new changes to an application, to validate new or upgraded hardware with an existing application, or to baseline the performance of a brand-new application on a brand-new hardware platform. The results of the load test are analyzed and interpreted in accordance with the change being tested.

# ### New Application

A new application does not allow you to compare the results of the load test with your current production environment. However, you can establish baseline performance metrics, analyze execution plans and data access patterns, collect instance data, collect OS and hardware performance data, and possibly even begin tuning. It is very difficult to compare functions such as accounts payable on one application to accounts payable on another application, since the application, the database schema, and the basic operational tasks are so different. However, this is a great starting point for collecting baseline data and beginning the tuning process.

# ### New Version of an Existing Application

A new version of an existing application provides more flexibility to compare the results of the load test with performance in your current production environment. With the new version, the basic results of functional tasks such as accounts payable should be comparable. In addition, the database schema should be similar. Here you should be able to make some comparisons. However, keep in mind that the new version might be providing greater functionality and more features. Thus, you might expect performance to be slightly slower than on the existing application.

# ### New Hardware with an Existing Application

Load testing works best in this type of environment, since you are replacing existing hardware with newer and, hopefully, faster hardware. You should expect performance to be better and response times to be faster. These expectations are based on assumptions that the newer hardware is faster than the existing hardware. This