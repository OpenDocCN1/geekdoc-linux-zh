
`Order allow,deny`

`Allow from all`

`</Directory>`

```
# ScriptAlias: 这控制哪些目录包含服务器脚本。
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

# "/var/www/cgi-bin/" 应该更改为你存在的 ScriptAliased
# CGI 目录，如果你配置了该项的话。
```

`<Directory "/var/www/cgi-bin">`

`AllowOverride None`

`Options None`

`Order allow,deny`

`Allow from all`

`</Directory>`
