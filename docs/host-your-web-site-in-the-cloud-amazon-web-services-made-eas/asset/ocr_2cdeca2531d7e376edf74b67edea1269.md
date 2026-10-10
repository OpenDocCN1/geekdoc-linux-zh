The group, called AutoScale, references the load balancer (LoadBal1) and the launch configuration (Conf1g). It'll run up to five instances in Availability Zone us-east-1b. Now we need a trigger. Here's the command to create a trigger named Trigger1:

```
```bash
$ as-create-or-update-trigger Trigger1 --auto-scaling-group
  AutoScale --namespace "AWS/EC2" --measure CPUUtilization
  --statistic Average --dimensions "AutoScalingGroupName=AutoScale"
  --units "Percent" --period 60 --lower-threshold 30
  --upper-threshold 70 --lower-breach-increment="-1"
  --upper-breach-increment "1" --breach-duration 120
OK-Created/Updated trigger
```
```

That's a fairly long command, so let's break it down. It's driven by the EC2 metric CPUUtilization. It will initiate a scale-out action when average CPU utilization for the set of EC2 instances in the group exceeds 70% over a two-minute interval. It will initiate a scale-in operation when the average CPU utilization falls below 30%, also over a two-minute interval. It will add one new instance on scale-out and remove one instance on scale-in.

Once the trigger has been set, the group becomes active. Here's how to see what's happening:

```
```bash
$ as-describe-scaling-activities AutoScale
ACTIVITY  a470869e-14d8-4b02-98f5-33e9a8b7afda  2009-07-25T04:53:33Z
  Successful  "At 2009-07-25 04:50:57Z a user request created an
  AutoScalingGroup changing the desired capacity from 0 to 1.
  At 2009-07-25 04:52:05Z an instance was started in response to a
  difference between desired and actual capacity, increasing the
  capacity from 0 to 1."
```
```

The as-describe-scaling-activities command displays the most recent scaling activities in reverse chronological order.

You should shut the group down cleanly once you're done with it. Here's how to do that. Start by deleting the trigger (you'll be asked to confirm):

```
```bash
$ as-delete-trigger Trigger1 --auto-scaling-group AutoScale
```
```

Next, set the minimum and maximum size of the group to zero to force all its instances to terminate: