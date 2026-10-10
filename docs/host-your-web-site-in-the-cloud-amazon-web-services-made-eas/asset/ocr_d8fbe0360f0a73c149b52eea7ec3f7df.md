+   3. an auto scaling group for the desired set of Availability Zones, supplying the names of the load balancer and the launch configuration, the desired minimum and maximum size of each group, and a reference name for the group
+   4. a trigger for the group

Then sit back and relax as the auto scaling process ensures that you have sufficient EC2 instances in place to meet your application’s requirements, as expressed in the group size and in the trigger.

Once an auto scaling group is up and running, it operates as follows:

+   1. The CloudWatch metrics specified in the group’s trigger are retrieved using the parameters (Namespace, Dimension, Measure, Statistic, and Unit) for a time range that extends back in time by the trigger’s BreachDuration value.
+   2. The metrics are checked against the trigger’s thresholds. If the metrics are larger than the UpperThreshold, and the number of EC2 instances in the group is less than the MaxSize, a scale-out event is initiated. One or more EC2 instances are launched using the group’s launch configuration parameters. The number of instances launched depends on the trigger’s UpperBreachScaleIncrement. If the value of this parameter ends with a percent sign (“%”) then sufficient instances are launched to raise the total number in the group by that percentage. Otherwise, the value is used as the actual number of instances to launch. New instances are automatically added to the load balancer (if any) associated with the group.

In similar fashion, if the metric is smaller than the LowerThreshold, and the number of instances in the group is more than MinSize, a scale-in event is initiated. One or more EC2 instances are terminated, again using the parameters from the group’s launch configuration. The number of instances terminated depends on the trigger’s LowerBreachScaleIncrement, which can be a percentage value or a number. In either case the numeric value should be negative. The excess instances are removed from the load balancer (if any) before they’re terminated.

After a scale-in or scale-out event, no further automatic scaling actions will be triggered until after the group’s cool-down period has passed. All the scale-in and scale-out events are logged and can be retrieved for later analysis.