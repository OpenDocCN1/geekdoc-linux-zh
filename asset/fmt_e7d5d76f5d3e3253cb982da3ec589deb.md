
某些版本的`ftp`比其他版本更啰嗦，当客户端和服务器之间出现不匹配时，某些`ftp`版本会产生类似“未实现命令”的错误。例如，在脚本中可以看到：

```
$ ftpget ftp://ncftp.com/ncftp/ncftp-3.1.5-src.tar.bz2
ftpget: Downloading ncftp-3.1.5-src.tar.bz2 from server ftp.ncftp.com
-rw-r-r-- 1 taylor taylor 394777 Jan 6 08:26 ncftp-3.1.5-src.tar.bz2
```
