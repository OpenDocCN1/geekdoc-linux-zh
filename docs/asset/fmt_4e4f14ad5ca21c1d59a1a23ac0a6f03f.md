
```c
mysql_escape_string(es, title, strlen(title));
sprintf(is, "INSERT INTO cd(title, artist_id, catalogue) VALUES ('%s', %d, '%s')", es, artist_id, catalogue);
res = mysql_query(&my_connection, is);
if (res) {
  fprintf(stderr, "Insert error %d: %s\n", mysql_errno(&my_connection), mysql_error(&my_connection));
  return 
```

当我们为这张 CD 添加曲目时，我们需要知道插入 CD 记录时使用的 ID。我们将该字段设置为自增，因此数据库会自动为我们分配一个 ID，我们需要显式地检索该值。我们在章节前面看到通过特殊函数 `LAST_INSERT_ID()` 实现这一点。

```c
res = mysql_query(&my_connection, "SELECT LAST_INSERT_ID()");
if (res) {
  printf("SELECT error: %s\n", mysql_error(&my_connection));
  return 0;
} else {
  res_ptr = mysql_use_result(&my_connection);
  if (res_ptr) {
    if ((mysqlrow = mysql_fetch_row(res_ptr))) {
      sscanf(mysqlrow[0], "%d", &new_cd_id);
    }
    mysql_free_result(res_ptr);
  }
}
```

我们不需要担心同时插入 CD 会导致 ID 混乱：MySQL 按连接跟踪 ID，即使另一个应用程序在我们检索 ID 之前插入了 CD，我们仍然会获取对应于我们行的的 ID。

最后，我们设置新添加行的 ID 并返回成功：

```c
*cd_id = new_cd_id;
if (new_cd_id != -1) return 1;
return 0;
}
/* add_cd */
```

现在来看 `get_artist_id` 的实现；该过程与插入记录非常相似：

```c
static int get_artist_id(char *artist) {
    MYSQL_RES *res_ptr;
    MYSQL_ROW mysqlrow;

    int res;
    char qs[100];
    char es[100];
    int artist_id = -1;

    /* 它已经存在了吗？ */
    mysql_escape_string(es, artist, strlen(artist));
    sprintf(qs, "SELECT id FROM artist WHERE name = '%s'", es);
    res = mysql_query(&my_connection, qs);
    if (res) {
        fprintf(stderr, "Select error: %s\n", mysql_error(&my_connection));
    } else {
        res_ptr = mysql_store_result(&my_connection);
        if (res_ptr) {
            if (mysql_num_rows(res_ptr) > 0) {
                if ((mysqlrow = mysql_fetch_row(res_ptr))) {
                    sscanf(mysqlrow[0], "%d", &artist_id);
                }
            }
            mysql_free_result(res_ptr);
        }
    }

    if (artist_id == -1) {
        /* 查找或创建 */
        sprintf(qs, "INSERT INTO artist (name) VALUES ('%s')", artist);
        res = mysql_query(&my_connection, qs);
        if (res) {
            fprintf(stderr, "Insert error: %s\n", mysql_error(&my_connection));
        } else {
            artist_id = mysql_insert_id(my_connection);
        }
    }
    return artist_id;
}
/* get_artist_id */
```

现在我们为我们的 CD 添加曲目信息。同样，我们对曲目标题中的特殊字符进行了保护：

```c
int add_tracks(struct current_tracks_st *tracks) {

    int res;
    char is[100];
    char es[100];
    int i;

    if (!dbconnected) return 0;

    i = 0;
    while (tracks->track[i]) {
        mysql_escape_string(es, tracks->track[i], strlen(tracks->track[i]));
        sprintf(is, "INSERT INTO cd (cd_id, track_id, title) VALUES (%d, %d, '%s')", tracks->cd_id, i + 1, es);
        res = mysql_query(&my_connection, is);
        if (res) {
            fprintf(stderr, "Insert error: %s\n", mysql_error(&my_connection));
            return 0;
        }
        i++;
    }
    return 1;
}
/* add_tracks */
```

现在我们根据给定的 CD 值检索 CD 信息。我们将使用数据库连接在检索 CD 信息的同时检索曲目 ID。这通常是良好的做法：数据库知道如何高效地执行查询，因此不要编写应用程序代码来完成这些，只需传递 SQL 查询让数据库处理。这样做可以为你节省精力，并让你的应用程序运行更高效，让数据库尽可能地完成大部分工作。
