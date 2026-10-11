# **Feature**

# AWS for Linux

# Go serverless

Serverless concepts are distinctly forward-thinking. Breaking your complex application into microservices can offer many benefits

All of the AWS services we've talked about so far are traditional server concepts. Recently, however, Amazon has been heavily promoting the 'serverless' model. As the name suggests, serverless computing allows you to build and run applications and services without thinking about servers. 

Serverless applications don't require you to provision, scale and manage any servers yourself. You can build the applications for virtually any type of use or back-end service and everything required to run and scale

your application with high availability is handled on your behalf by AWS. 

Building serverless applications means less time managing and operating servers or runtimes, removing the need to provision, update or administer servers. Serverless applications are also much more scalable, are designed with high availability in mind and, best of all, have no idle capacity. Resources are only provisioned (and therefore are only charged for) when actually in use, providing a major potential cost saving.

> **QUICK TIP**
> Free JIRA account
> Atlassian JIRA is normally a paid product, but if you create a Codestar deployment (which is included in the free AWS tier), you can activate a five-user JIRA account completely free of charge.

# **HOW TO**
Get started with S3

![](bbox=[0.07, 0.51, 0.48, 0.61])

+   1. **Create a bucket**
+   Getting started with S3 is incredibly easy using the web console. S3 stores items in 'buckets', each of which must have a unique name across the AWS platform. Click 'Create Bucket', enter a name, choose a region and accept the default properties.

![](bbox=[0.52, 0.51, 0.92, 0.61])

+   2. **Bucket access and options**
+   After your bucket is set up, you can access it using your root credentials or using a user you set up in the IAM, provided you grant access. In the properties page you can also enable static website hosting, providing access to bucket objects via a URL.

![](bbox=[0.07, 0.73, 0.48, 0.83])

+   3. **Enable versioning**
+   Versioning allows you to keep multiple versions of an object in a bucket. As well helping to avoid accidental overwriting/loss, it's required for some features. Use 'Events' to trigger SNS, SQS or Lambda events when things happen in your bucket.

![](bbox=[0.52, 0.73, 0.92, 0.83])

+   4. **Enable cross-region replication**
+   Cross-region replication enables you to add extra resilience to your S3 bucket. As well replicating the whole bucket or items with a specific prefix to any other region, you can also specify Infrequent access mode in the destination bucket to reduce duplicated costs.