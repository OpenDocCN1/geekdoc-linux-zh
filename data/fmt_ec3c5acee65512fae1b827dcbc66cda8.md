
`db2` `"select substr(constname,1,18), substr(tabname,1,18), substr(reftabschema,1,14), substr(reftab,1,14), deleterule, substr(fk_columns,1,14), substr(pk_columns,1,14) from syscat.references where tabschema = 'user'"`

```sql
db2 "select substr(tabname,1,18), parents, children from syscat.tables where tabschema = user and (parents) > 0 or children > 0) order by 2, 3 desc"
```

```sql
select tabname, parents, children from syscat.tables where tabschema = 'INSTnn' and (parents) > 0 or children > 0) order by 2, 3 desc;
```

### 运行选择语句并比对结果

4. 运行一个选择语句来获取 `TABNAME` 的 18 个字符，以及 `SYSCAT.TABLES` 中的 `PARENTS` 和 `CHILDREN` 列，其中 `TABSCHEMA` 等于你的用户名。按 `TABNAME` 排序结果并将输出重定向到名为 `richk.file` 的文件中。`SQL` 语句可以在名为 `richk.sql` 的文件中找到。将你的输出与 `richk.master` 文件进行比对。
确保你的输出与主输出之间没有差异，否则后续练习可能无法正常运行！

```bash
db2 -tf richk.sql > richk.file
```

```bash
more richk.file
```

`diff -w richk.file richk.master | more`

如果你没有看到输出（命令提示符立即返回），说明你的表定义与主文件匹配。
如果你看到任何输出（文件之间的行将以 '<' 或 '>' 开头），则存在不匹配的行。第一行将指示你输出中的信息，第一列将指示与我们的解决方案定义不同的表；第二列将指示该表作为从表涉及的关系数量；第三列将指示其作为父表涉及的关系数量。检查这些信息，回到练习中指导你设置的说明，并修改有问题的表（或其依赖表）以纠正问题。
回到此步骤并再次检查。

`contents of richk.sql`: `select substr(tabname,1,18), parents, children from syscat.tables where tabschema = user order by tabname`

### 在 Db2 命令行窗口中：

```bash
db2 -tf richk.sql > richk.file
```

```bash
more richk.file
```

```bash
fc /w richk.file richk.master | more
```

如果你看到以下消息：
`FC: no differences encountered\your table definitions match the master file.`
如果你看到任何输出，则文件之间存在不匹配的行。第一组行将指示你输出中的信息，第二组行将指示主输出的信息。第一列将指示与我们的解决方案定义不同的表；第二列将指示该表作为从表涉及的关系数量；第三列将指示其作为父表涉及的关系数量。
检查这些信息，回到练习中指导你设置的说明，并修改有问题的表（或其依赖表）以纠正问题。
回到此步骤并再次检查。

`contents of richk.sql`: `select substr(tabname,1,18), parents, children from syscat.tables where tabschema = user order by tabname`
