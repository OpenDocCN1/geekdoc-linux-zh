
`db2set registry_variable_name=new_variable`

在 UNIX 系统上，可以使用 `export` 命令代替 `set` 命令。根据您的操作系统，可能会使用 `DB2INSTANCE`、`DB2PATH`、`DB2NODE` 和 `DB2PROFILE`。要查看所有支持的注册变量列表，请执行 `db2set-lr` 命令。可以使用以下命令更改当前或默认实例的值：

```
db2set registry_variable_name=new_variable
```
