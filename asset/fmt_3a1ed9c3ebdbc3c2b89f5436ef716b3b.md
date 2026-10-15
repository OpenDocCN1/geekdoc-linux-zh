
# 服务商列表

| 服务商 | 套餐 | 电话 | 数量 | 价格 | 空间 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `Evolving` (`www.evolvinghosts.com`) | `Partner` | N/A | N/A | £39.99 | 3GB |
| `Evolving` (`www.evolvinghosts.com`) | `Home` | N/A | N/A | £54.99 | 2.5GB |
| `Evolving` (`www.evolvinghosts.com`) | `Business` | N/A | N/A | £99.99 | 5GB |
| `Evolving` (`www.evolvinghosts.com`) | `eCommerce` | N/A | N/A | £159.99 | 20GB |
| `Gaacom` (`www.gaacom.com`) | `Business Pro` | `800 542 7560` | 1 | £199 | 100GB |
| `Global` (`www.globalhosts.com`) | `Professional` | `44 652 7750` | 1 | £69.99 | 5GB |
| `Heart Internet` (`www.heartinternet.com`) | `Professional` | `44 652 7750` | 2 | £89.99 | 10GB |
| `Heart Internet` (`www.heartinternet.com`) | `Professional` | `44 652 7750` | 3 | £129.99 | Unlimited |
| `Hostway` (`www.hostway.com`) | `Silver` | `0840 180 1780` | 1 | £78.90 | 150MB |
| `Merolog` (`www.merolog.com`) | `Email Only` | N/A | N/A | £18 | 1GB |
| `Merolog` (`www.merolog.com`) | `Shared Package` | `014 312 330` | 1 | £58.75 | 25GB |
| `Merolog` (`www.merolog.com`) | `Professional Package` | `014 312 330` | 2 | £105.75 | 500GB |
| `Skymarket` (`www.skymarket.com`) | `Standard 1` | `000 321 778` | 1 | £29 | 1GB |
| `Skymarket` (`www.skymarket.com`) | `Standard 2` | `000 321 778` | 2 | £59 | 2GB |
| `Skymarket` (`www.skymarket.com`) | `Premium 1` | `000 321 778` | 3 | £99 | 10GB |
| `ServiceWise` (`www.serwebsite.com`) | `Personal` | `084 520 0716` | 1 | £25.30 | 10GB |
| `ServiceWise` (`www.serwebsite.com`) | `Professional` | `084 520 0716` | 2 | £126 | 40GB |
| `ServiceWise` (`www.serwebsite.com`) | `Reseller` | `084 520 0716` | 3 | £126 | 40GB |

# 问题与解答

网站：`www.linuxuser.co.uk`

电子邮箱：`linuxuser@imagine-publishing.co.uk`

# 问答

## 回答您的问题

向我们发送问题，我们将尽力回答！

![](img/78fc0912c436c898922acde3c325ec7a_89_0.png)

## 常见问题解答 (FAQ)

### 更新发行版

**Q：那么我如何自动更新我的发行版？**

A：某些发行版包含一个非常有用的更新器，例如 `Ubuntu`。当有可用更新时，它们通常会提示你，它将更新并安装任何必要的包，同时保留你的文件和设置。其他发行版没有这个过程，因此你需要备份文件并安装更新后的发行版。最好留意任何可能影响你特定系统的更新。

**Q：我使用的是 LTS（长期支持）版 `Ubuntu`，但没有显示升级。这是什么问题？**

A：请使用“软件更新管理器”（`Update Manager`）并检查“设置”。转到“更新”选项卡，寻找“通知我 `Ubuntu` 版本”的菜单，并将其更改为“任何”。

**Q：如果我不喜欢，可以回降级到之前的版本吗？**

A：不太可能。这非常危险，并且可能会破坏所有包以回到之前的状态；最佳解决方案是进行备份，以防你想要回滚。

## 分析此问题

我正在运行 `Ubuntu 15.04`，我在 `Ubuntu` 软件中心安装了“磁盘用量”（`Disk Usage`）。它安装正常，但我发现任何地方都找不到它。在“附件”菜单里没有，在应用程序文件夹里没有，在终端里也没有。我搜索了“`Ubuntu` 软件中心”来显示位置，但那里什么都没有。我重启了电脑。还是没有。我卸载了“磁盘用量分析器”并重新安装了。有人知道可能发生了什么吗？

`Above Disk Analyzer` 擅长分解存储空间的使用情况

在我们在“管理”中看到的系统中，它会出现在菜单中，具体是在“管理”分类下。你确定你安装了正确的包吗？它被称为 `` `GNOME usage` ``，在软件中心里它被称为 `` `usage analyzer` ``。

你可以尝试使用命令行安装它。打开终端并使用：

```bash
$ sudo apt-get install baobab
```

你可以在终端里直接用 `` `baobab` `` 使用，或者在你的系统中再看一眼。

`Steven Grayson90`

## 修复我的图表

我在 `CentOS 7` 上配合 `NGINX + PHP-FPM` 安装了 `Grafana`，是通过参考几个在线指南手动完成的。

一切似乎运行正常——但它并没有真正显示任何图表。它应该显示空间，但图片就是无法加载。由于某种原因，我在 `rectify` 中有数据：

```bash
# curl /var/log/nginx/www.domain.com/process-service-graph \
  -H "Content-Type: application/json" \
  -d "start=$1" \
  -d "end=$2" \
  -d "step=$3" \
  -d "value=$4"
```

`register 0`

```xml
<!-- 圆形数据库 -->
  <version>0023.0</version>
  <step>30s</step> <-->
  <lastupdate>1435996565</lastupdate>
  <timestamp>2015-06-07T19:44:25 UTC</timestamp>
```

```json
{
  "data": {
    "type": "gauge",
    "name": "heartbeat-60s",
    "min": 0,
    "max": 100
  }
}
```

日志中没有错误。

```text
process_data
service_data_file=/var/log/nginx/perferdata.log
service_data_file_template=$SERVICE_OUTPUT/$SERVICE_ID.PERFDATA
service_data_file_mode=master
service_data_file_perferdata_processing
service_data_file_processing=
process-service-graph
```

在模板中：

```text
def service name named-graph
action_url show.cgi?host=$HOSTNAME&service=$SERVICE
='graph'
oncmover=showGraphPopup("his")
onclickout=showGraphPopup()
```

## 远程拨号

我有点绝望了，我已经寻找了好几天解决方案，却一无所获（简直不敢相信只有我一个人这么想）
