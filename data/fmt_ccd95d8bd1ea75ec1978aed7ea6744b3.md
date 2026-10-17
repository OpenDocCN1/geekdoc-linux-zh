
# AppRF

AppRF 提供了应用程序分类和控制。它允许根据应用程序识别并管理流量，而不是基于端口号。以下章节描述了 AppRF 如何工作以及如何配置它来实现限制带宽、阻塞某些应用程序或优先处理流量等目标。

## Deep Packet Inspection（深度数据包检测）

DPI 是一种数据包过滤方法，它通过检查数据包的负载内容来识别协议、垃圾邮件和攻击。

`show dpi application`

| Name | ID | Category | Default Ports |
| :--- | :--- | :--- | :--- |
| abc-news | 2024 | web | tcp | 80/443 |
| adobe-connect | 929 | streaming | tcp | 80,443 |
| bittorrent | 1535 | peer-to-peer | tcp | 1024-65535 |
| dropbox | 779 | cloud-file-storage | tcp | 80,443 |
| google-groups | 56 | collaboration | tcp | 80,443 |
| craigslist | 1848 | web | tcp | 80 |

`show dpi category`

Application Categories

| Name | Category ID | Applied |
| :--- | :--- | :--- |
| antivirus | 1 | 0 |
| authentication | 2 | 0 |
| behavioral | 3 | 0 |
| cloud-file-storage | 4 | 0 |
| collaboration | 5 | 0 |
| encrypted | 6 | 0 |
| enterprise-apps | 7 | 0 |
| gaming | 8 | 0 |
| im-file-transfer | 9 | 0 |
| instant-messaging | 10 | 0 |
| mail-protocols | 11 | 0 |
| mobile | 23 | 0 |
| mobile-app-store | 12 | 0 |
| network-service | 13 | 0 |
| peer-to-peer | 14 | 0 |
| social-networking | 15 | 0 |
| standard | 16 | 0 |
| streaming | 17 | 0 |
| thin-client | 18 | 0 |
| tunneling | 19 | 0 |
| unified-communications | 20 | 0 |
| web | 21 | 0 |
| webmail | 22 | 0 |

Total application groups = 23

`show dpi application category antivirus`

List of Applications

| Name | App ID | App Category | Default Ports | Applied |
| :--- | :--- | :--- | :--- | :--- |
| fsecure | 2249 | antivirus | tcp | 80,443 | 0 |
| ghostsurf | 1107 | antivirus | tcp | 12200 | 0 |
| mcafee | 111 | antivirus | tcp | 80 | 0 |
