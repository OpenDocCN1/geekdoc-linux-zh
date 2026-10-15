
在这里，`-k` 的参数是 SSH 密钥 ID，最后一个参数是你随意分配的 droplet 短名称。一旦 droplet 完成启动，你就可以使用 `digitalocean` 登录：

```
$ digitalocean ssh usah-ubuntu

Droplet name provided. Droplet ID...done, 23754220 (ubuntu-16.04-x64)

Executing SSH on Droplet (ubuntu-16.04-x64)...

This droplet has a private IP, checking if you asked to use the Private IP...You didn't! Using public IP for ssh...

Attempting SSH: root@45.55.1.165

Welcome to Ubuntu 16.04 (GNU/Linux 4.4.0-28-generic x86_64)

root@usah-ubuntu:~#
```
