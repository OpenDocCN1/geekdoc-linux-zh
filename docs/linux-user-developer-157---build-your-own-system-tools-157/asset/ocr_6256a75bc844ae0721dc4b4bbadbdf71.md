# Automate Linux on AWS

How to quit babysitting your server farm and automate your cloud administration

![](bbox=[0.06, 0.26, 0.17, 0.42])

+   Filipe Martins & Anna Kobylinska
+   teamed up two decades
+   ago on a Linux box and
+   ended up in enterprise
+   IT, designing cloud
+   topologies, optimising
+   Linux APIs and managing
+   AWS deployments

Routine maintenance of Linux systems can wear anyone down, even without the need to keep an eye on one's public cloud expenses. As a result, automation is quickly emerging as the weapon of choice for Linux administrators in the quest for more adequate control of infrastructure and services.

Ready-to-use automation tools along with raw cloud APIs have managed to redefine server administration in the cloud. Whether you want to embrace full-blown programmatic orchestration with tools such as Chef, Puppet, Eucalyptus or Ansible, or to simply ensure a reasonable response time from a couple of servers in the cloud at an acceptable cost-to-benefit ratio, automation is the way to go.

For all its perceived benefits and sophistication, automation has one major downside: it cuts both ways. It can save you time and money if you know what you are doing, but it can also cost you dearly if you let it get out of hand.

Even so, automation clearly is a lot more rewarding than manual micro-management. When it comes to saving money by using self-configuring fleets of Spot Instances (the topic of this tutorial), nothing beats the lean-back-and-wait principle of AWS automation. May the force of the cloud be with you.

# *'Automate' your AWS savings*

One way you can 'automate' your time and cost savings on AWS is by submitting Spot Fleet requests for any number of Linux instances at, or below, your bid price.

A Spot Instance is the most cost-efficient type of capacity reservation for a virtual machine, a so-called EC2 instance. With Spot Instances, you set your own price. The downside is the risk of losing data. Amazon doesn't guarantee the requested capacity allotment, regardless of the price you set. Your instances can be terminated at any time. In most cases, the cost savings make it more than worth the hassle.

Spot Instances typically run computations and output their results into persistent storage. This way, users retain the results in the case of instance failure or termination.

A Spot Fleet is a collection of Spot Instances that Amazon manages on your behalf (no custom code necessary). A Spot Fleet could run a batch processing job, a Hadoop-based Big Data workflow, or an HPC grid computing job, for example.

By using a Fleet, you ensure that Amazon will negotiate the Spot price on your behalf and strive to maintain your desired capacity. There's no charge for Spot Fleet requests.

# Resoures

+   AWS root account
+   Python

![](bbox=[0.2, 0.56, 0.86, 0.91])