
## 2.6. 图像翻转脚本

```bash
root@debian7:~# cat /usr/local/bin/flip.pl
$count = 0;
$pid = $$;
while (<>) {
	chomp($_);
	if ($1 =~ /\.*jpg$/i) {
		$url = $1;
		system("/usr/bin/wget", "-q", "-O", "/var/www/images/$count.jpg");
		system("/usr/bin/mogify", "-flip", "/var/www/images/$count.jpg");
		print("http://127.0.0.1/images/$count.jpg\n");
	} elsif ($1 =~ /\.*gif$/i) {
		$url = $1;
		system("/usr/bin/wget", "-q", "-O", "/var/www/images/$count.gif");
		system("/usr/bin/mogify", "-flip", "/var/www/images/$count.gif");
		print("http://127.0.0.1/images/$count.gif\n");
	} elsif ($1 =~ /\.*png$/i) {
		$url = $1;
		system("/usr/bin/wget", "-q", "-O", "/var/www/images/$count.png");
		system("/usr/bin/mogify", "-flip", "/var/www/images/$count.png");
		print("http://127.0.0.1/images/$count.png\n");
	} else {
		print("\n");
	}
	$count++;
}
```

在 `/etc/squid/squid.conf` 中更改或添加以下行：

```
http_access allow localnet
http_port 3128 transparent
```

## 2.7. /var/log/squid

`squid` 的标准日志位置是 `/var/log/squid`。

脚本 `/usr/local/bin/flip.pl` 使用 `/var/www/images`，并且应该被 `squid` 服务器（使用用户 `proxy`）和 `apache2` 服务器（使用 `www-data`）访问。截图显示如何创建此目录、设置权限并让用户加入组。

```
root@debian7:~# mkdir /var/www/images
root@debian7:~# chown www-data /var/www/images
root@debian7:~# chmod 755 /var/www/images
root@debian7:~# usermod -aG proxy www-data
root@debian7:~# usermod -aG proxy
```

重启 `squid` 和 `apache2` 后测试运行正常。(img/1d499a6177836f6f088a9e2a53e11a14_45_0.png)

## 2.8. 访问控制

默认 `squid` 设置只允许 `localhost`。要为私网络范围启用访问，请在 `squid.conf` 中查找“INSERT YOUR RULE(S)”句子并添加类似下方所示的两行。

```
# INSERT YOUR RULE(S) TO ALLOW ACCESS FROM CLIENTS
acl company_network src 192.168.1.0/24
http_access allow company_network
```

## 2.9. 测试 squid

首先，确保运行中的 `squid` 可以访问互联网。

```
root@RHEL4 ~ # wget -q http://linux-training.be/index.html
root@RHEL4 ~ # ls -l index.html
-rw-r--r-- 1 root 2269 Sep 18 13:18 index.html
```

然后配置浏览器或客户端使用代理服务器，或者你可以为命令行程序设置 `HTTP_PROXY` 变量指向代理。

```
root@fedora ~ # export HTTP_PROXY=http://192.168.1.39:8080
root@ubuntu ~ # export http_proxy=http://192.168.1.39:8080
```

可以使用 `wget -q` 测试客户端以简化截图。

```
root@RHEL5 ~ # wget > /resolv.conf
root@RHEL5 ~ # wget -q http://www.linux-training.be/index.html
root@RHEL5 ~ # ls -l index.html
-rw-r--r-- 1 root 2269 Sep 18 20:08 index.html
```

## 2.10. 域名解析

你需要在 `squid` 上进行域名解析，但客户端不需要。

```
paul@RHEL5 ~ $ wget http://grep.be
--14:35:44-- grep.be
Resolving grep.be... failed: Temporary failure in name resolution.
paul@RHEL5 ~ $ export http_proxy=http://192.168.1.39:8080
paul@RHEL5 ~ $ wget http://grep.be
--14:35:49-- http://grep.be/
```

Connecting to `192.168.1.39:8080`... connected.

Proxy request sent, awaiting response... `200 OK`

Length: `5390 (5.3K) [text/html]`

Saving to: `'index.html.1'`

```
100%[=================>] 5,390 .-K/s  in 0.1s

14:38:29 (54.8 KB/s)  - 'index.html' saved [5390/5390]

[paul@RHEL5 ~]$
```

## Introduction to Squid

## Part II. MySQL Database

# Table of Contents

*   3. Introduction to SQL using MySQL ................................................................... 43
*   3.1. Installing MySQL ................................................................. 44
*   3.2. Accessing MySQL ................................................................. 45
*   3.3. MySQL Databases ................................................................. 47
*   3.4. MySQL Tables ................................................................. 49
*   3.5. MySQL Records ................................................................. 51
*   3.6. Joining Two Tables ................................................................. 54
*   3.7. MySQL Triggers ................................................................. 55

# 第3章：使用 MySQL 介绍 SQL

`MySQL` 是一个理解结构化查询语言（SQL）的数据库服务器。`MySQL` 由瑞典公司 `MySQL AB` 开发。首次发布于 1995 年。2008 年，`MySQL AB` 被 `Sun Microsystems` 收购（现由 `Oracle` 所有）。

`MySQL` 在结合 `php` 和 `apache` 使用的网站中（LAMP 服务器中的 `m`）非常流行，但 `MySQL` 也被用于拥有巨大数据库的组织，如 `Facebook`、`Flickr`、`Google`、`Nokia`、`Wikipedia` 和 `Youtube`。
