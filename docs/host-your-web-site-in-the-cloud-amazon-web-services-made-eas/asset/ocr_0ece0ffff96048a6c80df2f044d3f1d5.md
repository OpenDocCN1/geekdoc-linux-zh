through its paces using the command line tools. We'll review the programming model, once again leaving the actual code up to you.

# ## Auto Scaling Concepts

You can create auto scaling groups in any EC2 region using EC2's auto scaling feature. Each auto scaling group has a reference name and can span one or more Availability Zones. An auto scaling group relies on a launch configuration to provide the information needed to launch EC2 instances. A trigger attached to the group supplies the information needed to initiate a scaling activity. A **scaling activity** is generated each time an auto scaling group launches or terminates EC2 instances. Instances are added as part of a **scale-out event** and terminated as part of a **scale-in event**. Each group also has a minimum size and a maximum size.

An **Auto Scaling launch configuration** includes an AMI ID, the name of an EC2 key pair, a list of EC2 security groups, an EC2 instance type, and other information needed to launch EC2 instances as needed.

An auto scaling trigger references a CloudWatch metric such as EC2 CPUPutilization or elastic load balancing HealthyHostCount. The trigger also includes upper and lower threshold values and scaling increments. The scaling increments can be absolute ("add 1 more instance") or relative ("add 50% more instances"). The trigger's breach duration specifies the time period over which the trigger's thresholds are evaluated against the metrics.

# ## Auto Scaling Processing Model

Although auto scaling is independent of elastic load balancing, the two features were designed to work hand-in-glove to allow you to easily load balance large numbers of requests across an automatically scaled cluster of EC2 instances. Once everything is set up, you can simply route all your traffic to the load balancer and AWS will take care of the rest.

The auto scaling processing model is clean and easy to understand. To make a start, create the following:

+   1. an elastic load balancer for one or more Availability Zones
+   2. a launch configuration, specifying the ID of the AMI to be launched, the instance type, and other sought parameters