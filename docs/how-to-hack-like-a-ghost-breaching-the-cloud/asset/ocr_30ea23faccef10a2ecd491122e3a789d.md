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