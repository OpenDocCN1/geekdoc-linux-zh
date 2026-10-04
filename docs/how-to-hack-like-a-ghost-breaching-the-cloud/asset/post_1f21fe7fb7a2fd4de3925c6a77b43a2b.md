
At this stage, we have a pretty solid foothold on the Kubernetes cluster. We could go on spinning processes on random nodes in case someone destroys our Kube resources, but hopefully by that time we’ll already have finished our business anyway.

## Resources
- For more information about meterpreter payloads, search for the article “Deep Dive into Stageless Meterpreter Payloads” by OJ Reeves on https://blog.rapid7.com/.
- For a thorough article about the power of memcpy and mprotect for shell-code execution, see “Make Stack Executable Again” by Shivam Shrirao: http://bit.ly/3601dxh.
- The ReflectiveELFLoader by @nsxz provides a proof of concept: https://github.com/nsxz/ReflectiveELFLoader/. The code is well documented but requires some knowledge of ELF headers; see https://0x00sec.org/t/dissecting-and-exploiting-elf-files/7267/.
- A compilation of memory-only execution methods on Linux can be found at http://bit.ly/35YMiTY.
- Memfd was introduced in Linux kernel 3.17. See the manual page for memfd_create: http://bit.ly/3aeig27.
- For more information about DaemonSets, see the Kubernetes documentation: http://bit.ly/2TBkmD8.
- For help with Docker, see the API docs: https://dockr.ly/2QKr1ck.

## PART IV

## THE ENEMY INSIDE

> Gravity is not a version of the truth. It is the truth. Anybody who doubts it is invited to jump out of a tenth-floor window.
Richard Dawkins

## 10

## THE ENEMY INSIDE

![](img/961e81aef23040d0fbe348f58c055860_187_0.png)

In the previous chapter, we took over MXR Ads’ delivery cluster. This yielded hundreds of secrets, ranging from AWS access keys to GitHub tokens, promising access to pretty much any database involved in the delivery of an ad. We are not yet admins of the AWS account, but it’s barely a nudge away. We need to make sense of all the data we gathered and use it to find a way to escalate privileges, and even perhaps uncover the hidden link between MXR Ads and Gretsch Politico.

## The Path to Apotheosis

We load the AWS access keys we retrieved from Kube and check out the permissions of a random user. Kevin from Chapter 8, for instance, is as good a target as any:

```
root@Point1:~/# aws iam get-user --profile kevin
"User": {
  "UserName": "kevin.duncan",
--snip--
```

We know that, by default, IAM users have absolutely zero rights on AWS. They cannot even change their own passwords. Companies will therefore almost always grant users just enough rights on the IAM service that handles users and permissions to perform basic operations like changing passwords, listing policies, enabling multifactor authentication, and so on.

To limit the scope of these permissions, admins will often add a condition to accept IAM API calls targeting only the calling user. For example, Kevin is probably allowed to list his own permissions, but not those attached to other users:

```
root@Point1:~/# aws iam list-attached-user-policies \
--user-name=kevin.duncan \
--profile kevin

"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-self-manage",
"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-read-only",
"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-eks-admin"
```

Indeed, we get an error as soon as we call an IAM command on a resource other than Kevin, like so:

```
root@Point1:~/# aws iam get-policy \
--policy-arn mxrads-self-manage \
--profile kevin

An error occurred (AccessDenied) when calling the GetPolicy operation:
User: arn:aws:iam::886371554408:user/kevin.duncan is not authorized to
perform: iam:GetPolicy on resource: policy
arn:aws:iam::886371554408:policy/mxrads-eks-admin...
```

AWS runs a tight ship when it comes to access rights. Thankfully, the names of Kevin’s policies are explicit enough that we can guess their content: mxrads-eks-admin indicates Kevin is admin over the EKS, and mxrads-read-only probably confers Kevin read access to a subset of the 165 AWS services used by MXR Ads. It’s just a matter of trying to deduce which ones. The last policy, mxrads-self-manage, should contain the set of permissions for Kevin to manage his account.

Each of these services could take hours, even days, to fully explore, especially for a company so invested in AWS and with such a complex business architecture. We need to keep our focus straight: we’re looking for anything remotely related to Gretsch Politico—specifically information on their clients or data profiling activity. This might come in the form of an S3 bucket holding Digital Ad Ratings (DAR) segments (used to measure the performance of an advertising campaign), a table on an RDS database, a web server running on EC2, a proxy service on API Gateway, a messaging queue on AWS Simple Queue Service (SQS) . . . in any of the dozen AWS regions currently available. Yes, I feel and share your frustration.

Luckily, AWS has a useful API that spans multiple resource types and services in a given region: the Resource Groups Tagging API. This API returns S3 buckets, VPC endpoints, databases, and so on, provided that the object possesses a tag or a label. Any company with minimal infrastructure hygiene will make sure to tag its resources, if only for billing purposes, so we can be fairly confident that the results returned by this API call are accurate and comprehensive. We start by listing the resources for the eu-west-1 region, as shown in Listing 10-1.

```bash
root@Point1:~/# aws resourcegroupstaggingapi get-resources \
--region eu-west-1 \
--profile kevin > tagged_resources_euw1.txt

root@Point1:~/# head tagged_resources_euw1.txt

ResourceARN: arn:aws:ec2:eu-west-1:886371554408:vpc/vpc-01e638,
Tags: [ "Key": "Name", "Value": "privateVPC"]
--snip--
arn:aws:ec2:eu-west-1:886371554408:security-group/sg-07108...
arn:aws:lambda:eu-west-1:886371554408:function:tag_index
arn:aws:events:eu-west-1:886371554408:rule/asg-controller3
arn:aws:dynamodb:eu-west-1:886371554408:table/cruise_case
--snip--
```

*Listing 10-1: Listing resources for eu-west-1*

Had Kevin lacked the necessary privileges to list resource tags (tag:GetResources), we would have had no choice but to manually start exploring the most commonly used AWS services, such as EC2, S3, Lambda, RDS, DynamoDB, API Gateway, ECR, KMS, and Redshift. Redshift is a managed PostgreSQL optimized for analytics, DynamoDB is a managed nonrelational database modeled after MongoDB, API Gateway is a managed proxy that relays requests to the backend of your choice, and Lambda is a service that runs your code on AWS's own instances (more on that later). These primitive services are even used by AWS itself internally to build more complex offerings like EKS, which is in fact nothing more than the combination of EC2, ECR, API Gateway, Lambda, DynamoDB, and other services.

**NOTE** *There are many AWS auditing and pentesting tools that enumerate services and resources. Check out Toniiblyx's compilation on GitHub at https://github.com/toniblyx/my-arsenal-of-aws-security-tools/. Beware that most of these tools may flood AWS with API calls, an activity that can be picked up with minimal monitoring (more on that later).*

From Listing 10-1 we pulled well over 8,000 tagged resources from MXR Ads’ account, so naturally we turn to our trusted grep command to look for references to GP:

```
root@Point1:~# egrep -i "gretsch|politico|gpoli" tagged_resources_euw1.txt

ResourceARN: arn:aws:lambda:eu-west-1:886477354405:function:dmp-sync-gretsch-politico,
--snip--
```

Marvelous! There’s our hidden needle. MXR Ads has a Lambda function that seems to exchange data with Gretsch Politico. AWS Lambda is the gold standard of the serverless world. You package Python source code, a Ruby script, or a Go binary in a ZIP file, send it to AWS Lambda along with a few environment variables and CPU/memory specifications, and AWS runs it for you.

The process involves none of the hassle of machine provisioning, systemd setup, and SSH. You simply point to a ZIP file and it’s executed at the time of your choosing. A Lambda function can even be triggered by external events fired by other AWS services, like a file reception on S3. Lambda is a glorified crontab that has changed the way people orchestrate their workloads.

Let’s take a closer look at this dmp-sync Lambda function (see Listing 10-2).

```
root@Point1:~# aws lambda get-function \
--function-name dmp-sync-gretsch-politico \
--region eu-west-1 \
--profile kevin

--snip--
RepositoryType: S3,
Location: https://mxrads-lambdas.s3.eu-west-1.amazonaws.com/functions/dmp-sync-gp?versionId=YbSa...
```

Listing 10-2: Description of the dmp-sync Lambda function

We see in Listing 10-2 that the Lambda function retrieves the compiled code it needs to execute from the S3 path mxrads-lambdas/dmp-sync-gp. We immediately rush to the keyboard and start typing our next command:

```
root@Point1:~# aws s3api get-object \
--bucket mxrads-lambdas \
--key functions/dmp-sync-gp dmp-sync-gp \
--profile kevin

An error occurred (AccessDenied) when calling the GetObject operation:
Access Denied
```

But alas, Kevin is not trusted enough to be granted access to this bucket. We could build a wall with all the “Access Denied” messages we received over the last couple of days.
