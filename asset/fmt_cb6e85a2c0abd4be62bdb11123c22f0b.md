
# CGI 扫描路径列表

`/cgi-bin/info2www`
`/cgi-bin/jj`
`/cgi-bin/mailist.pl`
`/cgi-bin/man.sh`
`/cgi-bin/nph-test-cgi`
`/cgi-bin/perl.exe`
`/cgi-bin/pfdispaly.cgi`
`/cgi-bin/phf`
`/cgi-bin/php.cgi`
`/cgi-bin/test-cgi`
`/cgi-bin/Unlg1.1`
`/cgi-bin/view-source`
`/cgi-bin/webdist.cgi`
`/cgi-bin/webgais`
`/cgi-bin/websendmail`
`/cgi-bin/wwwboard.pl`
`/cgi-bin/www-sql`
`/cgi-dos/args.bat`
`/cgi-win/uploader.exe`

## 编译与运行

下载 CGI scanner v1.0 后，编译它：

```
$ cc cgichk-11b.c -o cghichk
```

然后运行它：

```
$ cgichk
```

## 扫描示例

以下是从 linux2 到 GNSS 的扫描示例：

```
[CKS & Fdisk]'s CGI Checker - modify by sh31 11.03.99
[ 按任意键检查 httpd 版本...... ]
HTTP/1.0 200 Document follows
Date: Tue, 01 Jun 1999 09:44:14 GMT
Server: NCSA/1.4.1
Content-type: text/html
[ 按任意键搜索 4 种 CGI 内容...... ]
Searching for Unlg : Not Found
Searching for phf : Not Found
Searching for Count.cgi : Not Found
Searching for test-cgi : Not Found
Searching for nph-test-cgi : Not Found
Searching for php.cgi : Not Found
Searching for handler : Found ;)
Searching for webgais : Not Found
Searching for websendmail : Not Found
Searching for webdist.cgi : Found ;)
Searching for faxesvey : Not Found
Searching for htmlscript : Not Found
Searching for pfdisplay : Not Found
Searching for perl.exe : Not Found
Searching for wwwboard.pl : Not Found
Searching for www-sql : Not Found
Searching for view-source : Not Found
Searching for campas : Not Found
Searching for aglimpse : Not Found
Searching for man.sh : Not Found
Searching for AT-admin.cgi : Not Found
Searching for filemail.pl : Not Found
Searching for maillist.pl : Not Found
Searching for jj : Not Found
Searching for info2www : Not Found
Searching for users.pwd : Not Found
Searching for args.bat : Not Found
Searching for uploader.exe : Not Found
...have a nice ;)
```

在这里，CGI scanner 发现了两个 IRIX 漏洞：

- `cgi-bin/handler` 脚本允许本地和远程用户以 httpd 守护进程权限执行任意命令。
- `weblist.cgi` 程序允许本地和远程用户以 httpd 守护进程权限执行任意命令。

CGI 扫描器适用于检查服务器经常被遗漏的漏洞。你可以通过添加新文件 `variables.cgi` 来快速向 CGI Scanner 添加新过程，例如：

```
buff[27] = "GET /_vvt/users.pwd HTTP/1.0"

buff[28] = "GET /_vvt/authors.pwd HTTP/1.0"

buff[29] = "GET /cgi-dos/args.bat HTTP/1.0"

buff[30] = "GET /cgi-win/uploader.exe HTTP/1.0"

buff[31] = "GET /cgi-bin/variables.cgi HTTP/1.0"
```

以及：

```
buff[26] = "service.pwd";

buff[27] = "users.pwd";

buff[28] = "authors.pwd";

buff[29] = '*args.bat';

buff[30] = '*uploader.exe';

buff[31] = '*variables.cgi';
```
