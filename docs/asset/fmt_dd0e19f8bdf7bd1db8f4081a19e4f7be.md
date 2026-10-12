
```
postgres=# \
             List of databases
  Name        Owner      postgres | UTF8    Encoding      Collate      Ctype       Access privileges
  confluence | postgres | UTF8    | en_US.UTF-8 | en_US.UTF-8 |
  postgres    | postgres | UTF8    | en_US.UTF-8 | en_US.UTF-8 |
  templated  | postgres | UTF8    | en_US.UTF-8 | en_US.UTF-8 |=c/postgres      +
  template   | postgres | UTF8    | en_US.UTF-8 | en_US.UTF-8 |=c/postgres      +

(4 行)
```

通过我们的端口转发使用 `psql` 连接到 `PGDDATABASE01` 服务。成功！我们通过端口转发连接到了数据库。我们还会发现我们有访问 `conformance` 数据库。使用我们的数据库，我们可以在 `conformance` 数据库中继续枚举，让我们查询 `cw_user` 表。它包含所有用户的用户名和密码哈希。我们将通过 `\c conformance` 连接数据库，然后运行 `select` 来查看所有内容。

```
postgres=# select * from cw_user;
| id | user_name | active | created_date | updated_date | first_name | last_name | lower_username | lower_first_name | lower_last_name | lower_display_name | email_address |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 5073 | admin | t | 2022-07-17 15:51:40 | 2022-07-17 | Alice | alice | alice | alice | alice@industries.internal |
| 5283 | alice | t | 2022-07-17 15:51:40 | 2022-07-17 | Alice | alice | alice | alice | alice@industries.internal |
| 2218 | template | t | 2022-08-10 16:31:48 | 2022-08-10 | template | template | template | template | template | template@industries.internal |
| 2761 | trouble | t | 2022-08-10 16:31:48 | 2022-08-10 | trouble | trouble | trouble | trouble | trouble@industries.internal |
| 22419 | happiness | t | 2022-08-10 13:33:49 | 2022-08-18 | happiness | happiness | happiness | happiness | happiness@industries.internal |
```
