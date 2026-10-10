```
```bash
$ mon-list-metrics
CPUUtilization AWS/EC2 {ImageId=ami-3c47a355}
CPUUtilization AWS/EC2 {InstanceType=m1.small}
CPUUtilization AWS/EC2
CPUUtilization AWS/EC2 {InstanceId=i-aaba69c3}
: a big long list...
```
```

The results are broken down by metric (DiskReadBytes, DiskReadOps, NetworkIn, NetworkOut, DiskWriteBytes, DiskWriteOps and so on) and denote the dimensions (ImageId, InstanceId, InstanceType, and so on) that may be requested from CloudWatch. Metrics are retained and can be retrieved for instances that you’ve recently terminated. Witness the following dimensions for CPU utilization below.

Here is the dimension for the CPU utilization of all your running or recently terminated EC2 instances:

```
```
CPUUtilization AWS/EC2
```
```

And this denotes the CPU utilization of running/recently terminated EC2 instances of type m1.small:

```
```
CPUUtilization AWS/EC2 {InstanceType=m1.small}
```
```

This is the same again, only it’s for those launched using the indicated AMI:

```
```
CPUUtilization AWS/EC2 {ImageId=ami-3c47a355}
```
```

And here it’s for the specific running or recently terminated EC2 instance:

```
```
CPUUtilization AWS/EC2 {InstanceId=i-aaba69c3}
```
```

Once you have chosen a dimension, you can use the `mon-get-stats` command to retrieve any metrics that you’d like. For example, all CPU utilization, by hour, for the last 24 hours:

```
```bash
$ mon-get-stats CPUUtilization --statistics Average
--start-time 2010-07-27 --end-time 2009-07-28 --period 3600
--namespace AWS/EC2
2009-07-18 00:00:00 60.0 5.9479999999999995 Percent
```
```