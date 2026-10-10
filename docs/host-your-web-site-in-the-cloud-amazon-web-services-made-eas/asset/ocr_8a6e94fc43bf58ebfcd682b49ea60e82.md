# # Amazon RDS Programming Model

As is always the case with AWS, each aspect of the Amazon Relational Database Service is available through web service APIs. You can also use command line tools and the AWS Management Console to access and manipulate your RDS resources. The current version (2.5) of CloudFusion does not support RDS, so the examples in this chapter will make use of the command line tools and the console. It’s worth examining RDS at the API level, so let’s do that now.

The `CreateDBInstance` function is used to create a new DB Instance. Other functions that operate on DB Instances include `DescribeDBInstances`, `ModifyDBInstance`, `RebootDBInstance`, and `DeleteDBInstance`.

Another set of functions are used to create and manipulate DB Snapshots. These include `CreateDBSnapshot`, `DescribeDBSnapshots`, `DeleteDBSnapshot`, `RestoreDBInstanceFromDBSnapshot`, and `RestoreDBInstanceToPointInTime`.

Functions for manipulating DB Parameter Groups include `CreateDBParameterGroup`, `DeleteDBParameterGroup`, `DescribeEngineDefaultParameters`, and `ModifyDBParameterGroup`.

Similarly, the functions for manipulating DB Security Groups include `CreateDBSecurityGroup`, `DescribeDBSecurityGroups`, `DeleteDBSecurityGroup`, `AuthorizeDBSecurityGroupIngress`, and `RevokeDBSecurityGroupIngress`.

The `DescribeDBEvents` function is used to gain access to the events produced by each of your RDS resources.

# ## Amazon RDS Pricing

Your use of the Amazon Relational Database Service is charged based on five usage dimensions: DB Instance hours, provisioned storage, storage I/O, backup storage, and data transfer.

# ### DB Instance Hours

Hourly pricing for the use of Single-AZ RDS DB Instances ranges from $0.11 to $3.10 per hour, as we saw in Table 9.1. Pricing for Multi-AZ DB Instances is double what’s shown in the table, but this price covers both your primary DB Instance and the associated standby.