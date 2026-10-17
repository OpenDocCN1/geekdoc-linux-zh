
```text
['podman', '-version']

podman version: 3.0.4
```

```text
=GF_AUTH_ANONYMOUS_ORG_ROLE=Admin
```

```text
26. [grafana] | logger=settings t=2023-10-06T17:41.5038721892Z level=info msg="Target target=[all]"
27. [grafana] | logger=settings t=2023-10-06T17:41.5038754559Z level=info msg="Path Home" path=/usr/share/grafana
28. [grafana] | logger=settings t=2023-10-06T17:41.503876685Z level=info msg="Path Data" path=/var/lib/grafana
29. [grafana] | logger=settings t=2023-10-06T17:41.5038728252Z level=info msg="Path Logs" path=/var/log/grafana
30. [grafana] | logger=settings t=2023-10-06T17:41.5038791022Z level=info msg="Path Plugins" path=/var/lib/grafana/plugins
31. [grafana] | logger=settings t=2023-10-06T17:41.503880761Z level=info msg="Path Provisioning" path=/etc/grafana/provisioning
32. [grafana] | logger=settings t=2023-10-06T17:41.5038820186Z level=info msg="App mode production"
33. [grafana] | logger=sqlalchemy t=2023-10-06T17:41.5039735164Z level=info msg="Connecting to DB" dbtype=sqlite3
34. [grafana] | logger=migrator t=2023-10-06T17:41.5078509328Z level=info msg="Starting DB migrations"
35. [grafana] | logger=migrator t=2023-10-06T17:41.5074556085Z level=info msg="migrations completed" performed=0 skipped=493 duration=2.093629ms
36. [grafana] | logger=secrets t=2023-10-06T17:41.507514303
```

在我们的 `docker-compose` 文件中，我们有一些非常有趣的设置。其中之一是 `volume`（卷）。这将创建一个名为 `grafana` 的本地文件夹，我们将配置保存在这个文件中。这就是我们如何将宿主机上的本地文件夹挂载到容器中。另一部分是 `ports`（端口）。这告诉我们，外部端口 3000 并不是我们自己的，而是我们位于 3000 端口的 `grafana`。这就是我们从外部连接到服务的方式。

在接下来的文件中，我们可以看到端口映射：

```text
- 1. volume: ./grafana:/var/lib/grafana
- 2. ports:

# 4. - "3000:3000"
```

现在，当 Grafana 运行时，请验证你是否可以通过 `http://服务器IP地址:3000` 访问 Grafana GUI。

现在，我们可以将 Prometheus 添加到我们的技术栈中。在我们的监控文件夹中，创建一个名为 `prom` 的新文件夹，并在该文件夹中创建我们的 `prometheus.yaml` 配置文件，如下：

```text
1. root@pihole:~/opt/monitoring# cat prom/prometheus.yml
2. # 我的全局配置
3. global:
4. scrape_interval: 15s # 默认每 15 秒抓取一次目标。
5. evaluation_interval: 15s # 默认每 15 秒抓取一次目标评估。
6. # scrape_timeout 设置为全局默认值 (10s)。
7.
8. # 在与外部系统（联邦、远程存储、Alertmanager）通信时，
9. 将这些标签附加到任何时间序列或告警：
10. external_labels:
11. monitor: 'my-project'
12.
13. 每隔 'evaluation_interval' 秒加载并评估此文件中的规则。
14. rule_files:
15. - 'alert.rules'
16. # - "first.rules"
17. # - "second.rules"
18.
19. #告警
20. alerting:
21. alertmanagers:
22. - scheme: http
23. static_configs:
24.   - targets:
25.     - "alertmanager:9093"
26.
27. # 包含精确一个端点的抓取配置。
28. # 这里是 Prometheus 本身。
29. scrape_configs:
30.   # 任务名称将作为标签 job_name 添加到从此配置抓取的任何时间序列中。
31. - job_name: 'prometheus'
32.   # 抓取配置
```
