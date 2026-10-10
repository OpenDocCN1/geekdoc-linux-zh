

start-stop-daemon --start --quiet --pidfile /var/run/$NAME.pid \
--exec $DAEMON -- $DAEMON_OPTS || true
echo "$NAME."
;;

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_0.png)

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_1.png)

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_2.png)

## 1.5 使用 checkinstall 包跟踪安装脚本创建或修改的所有文件

checkinstall 包（见图 1.19）会跟踪安装过程中创建或修改的所有文件。它还会创建并安装一个与你的包管理器兼容的包（.deb 或 .rpm）（见图 16 和 17），如果你不再需要该包，以后可以用它来完全移除。有关其使用细节，请查阅附带的手册页。

```
gacanepa@ubuntuOS:~/nginx-1.5.6$ sudo aptitude install checkinstall
[sudo] password for gacanepa:
The following NEW packages will be installed:
build-essential[?] checkinstall dpkg-dev[?] fakeroot[?] g++[?] g++-4.6[?] libalgorithm-diff-perl[?] libalgorithm-diff-xs-perl[?] libalgorithm-merge-perl[?] libdpkg-perl[?] libstdc++6-4.6-dev[?]
0 packages upgraded, 11 newly installed, 0 to remove and 72 not upgraded.
Need to get 9,326 kB of archives. After unpacking 27.7 MB will be used.
Do you want to continue? [Y/n/?] Y
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_14_3.png)

```
gacanepa@ubuntuOS:~/nginx-1.5.6$ sudo checkinstall -D make install
checkinstall 1.6.2, Copyright 2009 Felipe Eduardo Sanchez Diaz Duran
this software is released under the GNU GPL.

The package documentation directory ./doc-pak does not exist.
Should I create a default set of package docs? [y]: y
Preparing package documentation...OK
```

图 1.20：使用 checkinstall 和 make install 创建 .deb 文件（I）

```
Done. The new package has been installed and saved to
/home/gacanepa/nginx-1.5.6/nginx_1.5.6-1_i386.deb
You can remove it from your system anytime using:
dpkg -r nginx
```

图 1.21：使用 checkinstall 和 make install 创建 .deb 文件（II）

当我们运行 `aptitude search nginx` 时，刚刚安装的包将会出现，并带有我们添加的描述注释（见图 1.22）：

```
gacanepa@ubuntuOS:~/nginx-1.5.6$ aptitude search nginx
i   nginx                                   - Nginx v1.5.6
p   nginx-common                            - small, but very powerful and efficient web server (co
p   nginx-doc                               - small, but very powerful and efficient web server (co
```

图 1.22：截图

## 1.6 在 CentOS 6.4 中安装 Nginx

### 1.6.1 从软件仓库安装

- 从 `http://nginx.org/packages/centos/6` 下载并安装 nginx yum 配置文件。请确保选择了正确的架构；`"noarch"` 是一个安全的选择：
  - 下载：`wget http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm`
  - 安装：`rpm -ivh nginx-release-centos-6-0.el6.ngx.noarch.rpm`
  - 安装 nginx：`yum install nginx`
  - 启动 nginx：`service nginx start`

### 1.6.2 从源代码安装

遵循与 Debian 和 Ubuntu 相同的步骤。

### 1.6.3 启用模块

根据其 wiki（NGINX Wiki 页面），Nginx 模块必须在编译时选择，因为目前不支持运行时选择模块。有关编译时选项的完整摘要（包括可选模块），可以通过运行 `./configure --help` 在提供的 configure 脚本中找到。不幸的是，如果我们已经安装了 Nginx 并希望添加某个模块，我们将不得不卸载它，然后重新编译以支持所需的模块。

标准 HTTP 模块列表请参考表 1（NGINX 模块）：

表 1.1：标准 HTTP 模块

| 名称 | 描述 | 版本 | 启用 configure 参数 |
| :--- | :--- | :--- | :--- |
| Map | 使用任意键/值对设置配置变量。 | 0.3.16 | --without-http_map_module |
| Memcached | Memcached 支持。 | | --without-http_memcached_module |
| Proxy | 代理到上游服务器。 | | --without-http_proxy_module |
| Referer | 根据 Referer 头部过滤请求。 | | --without-http_referer_module |
| Rewrite | 使用正则表达式重写请求。 | | --without-http_rewrite_module |
| SCGI | SCGI 协议支持。 | 0.8.42 | --without-http_scgi_module |
| Split Clients | 根据某些条件拆分客户端 | 0.8.37 | --without-http_split_clients_module |
| SSI | 服务器端包含。 | | --without-http_ssi_module |
| Upstream | 用于负载均衡。 | | --without-http_upstream_ip_hash_module<br>(仅 ip_hash 指令) |
| User ID | 发出标识 cookie。 | | --without-http_userid_module |
| uWSGI | uWSGI 协议支持。 | 0.8.40 | --without-http_uwsgi_module |
| X-Accel | 类似 X-Sendfile 的模块。 | | |

可选 HTTP 模块列表请参考表 2：

表 1.2：可选 HTTP 模块

| 名称 | 描述 | 版本 | 启用 configure 参数 |
| :--- | :--- | :--- | :--- |
| Addition | 向页面追加文本。 | | --with-http_addition_module |
| Auth Request | 基于子请求结果实现客户端授权。 | 1.5.4 | --with-http_auth_request_module |
| Degradation | 允许在低内存条件下为某些位置返回 204 或 444 代码。 | 0.8.25 | --with-http_degradation_module |
| Embedded Perl | 在 Nginx 配置文件中 Perl。 | 0.3.21 | --with-http_perl_module |
| FLV | Flash Streaming Video | 0.4.7 | --with-http_flv_module |
| GeoIP | 创建包含来自 MaxMind GeoIP 二进制文件信息的变量。 | 0.8.6, 0.7.63 | --with-http_geoip_module |
| Google PerfTools | Google Performance Tools 支持。 | 0.6.29 | --with-google_perftools_module |
| Gzip Precompression | 提供静态文件的预压缩版本。 | 0.6.23 | --with-http_gzip_static_module |
| Gunzip | 即时解压 gzip 压缩的响应。 | 1.3.6 | --with-http_gunzip_module |
| Image Filter | 使用 Libgd 转换图像 | 0.7.54 | --with-http_image_filter_module |
| MP4 | 启用具有寻址能力的 mp4 流媒体。 | 1.1.3, 1.0.7 | --with-http_mp4_module |
| Random Index | 随机化目录索引。 | 0.7.15 | --with-http_random_index_module |
| Real IP | 用于将 nginx 作为后端 | 0.3.8 | --with-http_realip_module |
| Secure Link | 使用密钥保护页面 | 0.7.18 | --with-http_secure_link_module |
| SSL | HTTPS/SSL 支持。 | | --with-http_ssl_module |
| Stub Status | 查看服务器统计信息。 | 0.1.18 | --with-http_stub_status_module |
| Substitution | 替换页面中的文本 | | --with-http_sub_module |
| WebDAV | WebDAV 直通支持。 | 0.3.38 | --with-http_dav_module |
| XSLT | 使用 XSLT 后处理页面。 | 0.7.8 | --with-http_xslt_module |

邮件模块列表请参考表 3：

表 1.3：邮件模块

| 名称 | 描述 | configure 参数 |
| :--- | :--- | :--- |
| Mail Core | 邮件模块核心参数。 | --with-mail |
| POP3 | POP3 设置。 | --without-mail_pop3_module |
| IMAP | IMAP 设置。 | --without-mail_imap_module |
| SMTP | SMTP 设置。 | --without-mail_smtp_module |
| Auth HTTP | 使用 Nginx 验证邮件服务。 | |
| Proxy | Nginx 可以代理 IMAP、POP3 和 SMTP 协议。 | |
| SSL | 此模块确保 POP3/IMAP/SMTP 的 SSL/TLS 支持。 | --with-mail_ssl_module |

作为一个例子，我们将重新编译 Nginx 以包含 Addition 模块（见图 1.23）：

![](img/3adf2b91cc40e3d0012eab041f055ca8_18_0.png)

图 1.23：使用 Addition 模块重新编译 Nginx

## 1.7 将 Nginx 添加为系统服务

- Debian / Ubuntu：`update-rc.d -f nginx defaults`（在 Ubuntu 上使用 sudo）

注意：如果 /etc/rcrunlevel.d/[SK]?name 中已存在任何文件，则 update-rc.d 不会执行任何操作。该程序之所以这样编写，是因为它永远不会更改可能由系统管理员自定义的现有配置。该程序只有在链接不存在时才安装链接，即看起来该服务从未被安装过。

- CentOS：`chkconfig nginx on`

# 第 2 章

# Nginx 配置指南

### 2.1 配置文件语法

根据 Merriam-Webster 在线词典，单词 syntax 代表“单词组合成短语、从句或句子的方式”。当然，这个定义取自词典，是针对英语（或实际上任何其他语言）学习者的。那么，来自不同背景、语言和国家的 IT 人士呢？上下文的变化并没有显著改变该术语的含义。特别是，配置文件的语法必须是正确的，正如解析它的程序所看到的那样，以便它能高效地工作。

我们将学习如何理解以及如何编写（和/或修改）Ubuntu 12.04 LTS 下 Nginx 的配置文件。这将通过指定一组定义 web 服务器行为的值来实现。

### 2.2 配置指令

默认情况下，Nginx 的行为由其主配置文件定义，该文件位于（正如之前所见，除非我们修改了此设置）`/usr/local/nginx/conf/nginx.conf`。该文件由一组指令组成，这些指令组织在一个非常易于理解其逻辑结构中（见图 2.1）。

