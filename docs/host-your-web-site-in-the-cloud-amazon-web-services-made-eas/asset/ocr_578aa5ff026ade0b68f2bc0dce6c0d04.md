# Amazon CloudWatch Pricing

There's a charge of $0.015 (1.5 cents) per hour per monitored EC2 instance for the use of CloudWatch. This charge covers monitoring, data storage, and access to the stored data using the command line tools and the CloudWatch API.

There's no charge for the storage or use of elastic load balancer data in CloudWatch.

# Amazon CloudWatch from the Command Line

The easiest way to put CloudWatch through its paces is to use the command line. There's one interesting twist that you need to be aware of, though. The EC2 tools are used to enable or disable CloudWatch for an EC2 instance. The CloudWatch tools are used to access the collected data.

Here is how to enable CloudWatch for a single EC2 instance. The first step is to determine the instance's ID using the `ec2-describe-instances` command:

```
$ ec2-describe-instances
INSTANCE i-aaba69c3 ami-2b5fb42 ec2-75-101-154-199.compute-1.amazonaws.com domU-12-31-38-00-A0-01.compute-1.internal running gsg-key-air 0 m1.small 2008-07-13T03:44:43+0000 us-east-1a aki-a71cf9ce i-ari-a51cf9cc monitoring-disabled
```

In this case the instance ID is `i-aaba69c3`. With this value in hand, the `ec2-monitor-instances` command is used to enable CloudWatch (substituting the ID of your own instance, of course):

```
$ ec2-monitor-instances i-aaba69c3
i-aaba69c3 monitoring-pending
```

This command can be run again (after a short delay) to confirm that CloudWatch has been enabled for the specified instance:

```
$ ec2-monitor-instances i-aaba69c3
i-aaba69c3 monitoring-enabled
```

The `mon-list-metrics` command (from the CloudWatch tools) displays the list of available metrics: