
# 安装 Litespeed 后的 php.ini 设置教程

> 原文：<https://blog.eldernode.com/tutorial-php-ini-settings-after-install-litespeed/>

![Tutorial php.ini Settings after install Litespeed](img/8b3ce2a10d9e3cca8b10b0fbb0e567f6.png)

加快网站速度和优化网站性能是用户最为关注的问题。这样做的原因在于，一方面用户能够更快地访问网站，另一方面搜索引擎也将此视为网站的一大优势。为了提升网站速度，各种解决方案层出不穷，其中一种方法就是使用`Litespeed`Web服务器并优化网站缓存管理。因此，在本文中，我们将教你如何在安装`Litespeed`后添加`php.ini`设置。此外，如果你想购买 [Linux VPS](https://eldernode.com/linux-vps/) 主机，可以访问 [Eldernode](https://eldernode.com/) 中的套餐。

## 安装 Litespeed 后如何添加 php.ini 设置

安装`Litespeed`后，将之前的`php.ini`文件链接到`Litespeed`的`php.ini`，以确保之前的设置不会被更改。

使用`php --ini`命令，找到当前`php.ini`的路径，并按照以下方式创建符号链接：

```
ln -s /usr/local/php56/lib/php.ini /usr/local/lsws/lsphp5/lib/php.ini
```

`php7`对应的`php.ini` Litespeed路径如下：

```
/usr/local/lsws/lsphp7/lib/
```

最后，通过以下命令重置`Litespeed`服务：

```
service lsws restart
```
