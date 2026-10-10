The EC2 Elastic Load Balancer allows you to distribute web traffic across any number of EC2 instances. The instances can be in the same Availability Zone or they can be scattered across several zones in a Region. The elastic load balancer performs periodic health checks on the instances that it manages, and will stop sending traffic to any instances it determines to be unhealthy. The health check consists of a configurable ping to each EC2 instance.

Finally, the EC2 Auto Scaling feature uses the data collected by CloudWatch to help you build a system that can scale out (adding more EC2 instances) and scale in (shutting down EC2 instances) within a defined auto scaling group. Auto scaling lets you define triggers for each operation. For example, you can use Auto Scaling to scale out by 10% when the average CPU utilization across the auto scaling group exceeds 80%, and then scale in by 10% when the CPU utilization drops below 40%.

# # Amazon Elastic MapReduce

The Elastic MapReduce service gives you the ability to use a number of EC2 instances running in parallel for large-scale data processing jobs. This service uses the open source Hadoop framework, an implementation of the MapReduce paradigm. Invented by Google, MapReduce isolates you from many of the issues that arise when you need to launch, monitor, load (with data), and terminate dozens or even hundreds of instances. Elastic MapReduce works just as well for pedestrian tasks, such as log file processing, as it does for esoteric scientific applications, such as gene sequencing.

# ## Other Services

AWS gains new features and services with great regularity. To stay up to date with the latest and greatest happenings, you should check the AWS home page and the AWS Blog (written by yours truly) from time to time.