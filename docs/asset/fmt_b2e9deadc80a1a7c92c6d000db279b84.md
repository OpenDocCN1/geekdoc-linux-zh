
`--with-apxs=/www/bin/apxs`

```bash
--with-mysql=/usr/local/mysql \
--enable-ftp \ 
--enable-trans-sid
```

## 4. 修改权限、配置、编译并安装，然后拷贝你的 INI 文件：

```bash
chmod 755 php_install
./php_install
cd php-5.0.0
make
make install
cp php.ini-di-dist /usr/local/lib/php.ini
```

## 5. 完成最后一步，你需要通过编辑 `httpd.conf` 文件为 Apache 添加 PHP 支持。请在文件末尾添加如下：

```
AddType application/x-httpd-php .php3
AddType application/x-httpd-php-source .phps
```

## 6. 将你的 `DirectoryIndex` 设置从

```
DirectoryIndex index.html
```
