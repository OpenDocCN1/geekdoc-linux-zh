

## 40. 发送电子邮件

你可以使用'smtplib'模块，通过SMTP（简单邮件传输协议）客户端接口发送电子邮件。

```
smtplib.SMTP([host [, port]])
```

示例（使用Google Mail SMTP服务器发送电子邮件）：

```
import smtplib
# Use your own to and from email address
fromaddr = 'kunaldeo@gmail.com'
toaddrs = 'toemail@gmail.com'
msg = 'I am a Python geek. Here is the proof!'
# Credentials
# Use your own Google Mail credentials while running the program
username = 'kunaldeo@gmail.com'
password = 'xxxxx'
# The actual mail send server = smtplib.SMTP('smtp.gmail.com:587')
# Google Mail uses secure connection for SMTP connections server.starttls()
server.login(username,password)
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
```

## 41. 访问FTP服务器

'ftplib'是Python的一个功能完备的FTP客户端模块。要建立FTP连接，可以使用以下函数：

```
ftplib.FTP([host [, user [, passwd [, acct [, timeout]]]]])
```

示例：

```
host = "ftp.redhat.com"
username = "anonymous"
password = "kunaldeo@gmail.com"
import ftplib
import urllib2
ftp_serv = ftplib.FTP(host,username,password)
# Download the file
u = urllib2.urlopen("ftp://ftp.redhat.com/pub/redhat/linux/README")
# Print the file contents
print (u.read())
```

输出：

```
[~/src/python $] python ftpclient.py
```

Red Hat Linux的旧版本已移至以下位置：ftp://archive.download.redhat.com/pub/redhat/linux/

## 42. 使用默认网页浏览器打开网页

'webbrowser'模块提供了一种便捷的方式，可以使用默认网页浏览器打开网页。

示例（使用系统的默认网页浏览器打开google.co.uk）：

```
>>> import webbrowser
>>> webbrowser.open("http://google.co.uk")
True
```

## 43. 创建安全哈希

'hashlib'模块支持多种安全哈希算法，包括SHA1、SHA224、SHA256、SHA384、SHA512和MD5。

示例（创建给定文本的十六进制摘要）：

```
>>> import hashlib
# sha Digest
>>> hashlib.sha1("M16 Classified Information 007").hexdigest()
'e22b154c7329cc0b935aeleb9593 18balb0c85'
# sha224 Digest
>>> hashlib.sha224("M16 Classified Information 007").hexdigest()
'3d8e1274100b2b2048842790e5eb97 7d59b40b998e355e2c'
# sha256 Digest
>>> hashlib.sha256("M16 Classified Information 007").hexdigest()
'2fd573d53fa7b67f2c39725991c89 b25607c7b4c6403e fdb3b1c19825e'
# sha384 Digest
>>> hashlib.sha384("M16 Classified Information 007").hexdigest()
'5c9416103fd1bd1e14d8ce1e3a1d5a29d99 dc192ed18aa7628b009884aafaa54b0e 9e0fc3d3a65c8b6c35372d'
# sha512 Digest
>>> hashlib.sha512("M16 Classified Information 007").hexdigest()
'a704ac3dbe6e8235784823a31d5a29d25 2c8221f4973f45b9f222aedc6a29b89077 8ea0b7a0a9ec4f8b1856614667fba7 3aldcf1ff92e48c712b2'
# MD5 Digest
>>> hashlib.md5("M16 Classified Information 007").hexdigest()
'e8e2fc52ca146f99a670c826f7126'
```

## 44. 为随机数设置种子

你可以使用'random'模块生成各种随机数。最常用的是'random.seed(x)'。它会初始化基本的随机数生成器。如果省略x或x为None，则使用当前系统时间：在首次导入该模块时，也会使用当前系统时间来初始化生成器。

## 45. 处理CSV（逗号分隔值）文件

CSV文件在网页上的数据交换中非常流行。使用'csv'模块，你可以读写CSV文件。

示例：

```
import csv
# write stocks data as comma-separated values
writer = csv.writer(open('stocks.csv', 'wb', buffering=0))
writer.writerow([
('GOOG', 'Google, Inc.', 505.24, 0.47, 0.05),
('YHOO', 'Yahoo Inc.', 27.38, 0.33, 1.22),
('CNET', 'CNET Networks, Inc.', 8.62, -0.13, -1.49)
])
# read stocks data, print status messages
stocks = csv.reader(open('stocks.csv', 'rb'))
status_labels = {-1: 'down', 0: 'unchanged', 1: 'up'}
for ticker, name, price, change, pct in stocks:
    status = status_labels[cmp(float(change), 0.0)]
    print('%s is %s (%.2f)' % (name, status, pct))
```

## 47. 使用setuptools安装第三方模块

'setuptools'是一个Python包，让你可以非常轻松地下载、构建、安装、升级和卸载包。

要使用'setuptools'，你需要从发行版的软件包管理器中安装。安装后，你可以使用'easy_install'命令执行Python包管理任务。

