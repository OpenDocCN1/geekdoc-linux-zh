
`exec sql SELECT genre_id INTO :genre_id, :genre_id_ind FROM genre WHERE`

`genre_name = :genre_name;`

`if (sqlca.code < 0 || genre_id_ind == 0) {`

`pg_print_debug(__FILE__, __LINE__, "Unknown genre");`

`exec sql ROLLBACK;`

`return DVD_ERR_RE;`

`}`

`exec sql INSERT INTO title (title_text, asin, director, genre_id, classification, actor1, actor2, release_date, rental_cost)`

`VALUES (:title_text, :asin, :director, :genre_id, :classification, :actor1, :actor2, :release_date, :rental_cost);`

`if (sqlca.code < 0) {`

`pg_print_debug(__FILE__, __LINE__, "insert title failed");`

`exec sql ROLLBACK;`

`return DVD_ERR_TABLE;`

`}`

`exec sql COMMIT;`

`return DVD_SUCCESS;`

`}`

### /* pg_title_get */

这是获取包含标题详情结构体、找到合适的 `genre_id` 并将行添加到 `title` 表的代码。

```c
int pg_title_get(int req_title_id, dvd_title *title_ptr) {
title_id = req_title_id;
exec sql SELECT title_id, title_text, asin, director, genre_name, classification, actor1, actor2, release_date, rental_cost
INTO :title_id, :ind_title_id, :title_text, :asin, :director, :genre_name, :classification, :actor1, :actor2, :release_date, :rental_cost
FROM title, genre WHERE title.title_id = :title_id AND title.genre_id = :genre_id;
if (sqlca.code < 0) {
  pg_print_debug(__FILE__, __LINE__, "title failed");
  exec sql ROLLBACK;
  return DVD_ERR_TABLE;
}
if (sqlca.code == 100 || ind_title_id == 0) {
  pg_print_debug(__FILE__, __LINE__, "title failed - no entry");
  exec sql ROLLBACK;
  return DVD_ERR_NOT_FOUND;
}
title_ptr->title_id = title_id;
strcpy(title_ptr->title_text, title_text);
strcpy(title_ptr->asin, asin);
strcpy(title_ptr->director, director);
strcpy(title_ptr->genre, genre_name);
strcpy(title_ptr->classification, classification);
strcpy(title_ptr->actor1, actor1);
strcpy(title_ptr->actor2, actor2);
strcpy(title_ptr->release_date, release_date);
strcpy(title_ptr->rental_cost, rental_cost);
exec sql COMMIT WORK;
return DVD_SUCCESS;
}
```

### /* pg_title_search */

另一个处理标题的“有趣”代码部分是搜索。API 允许客户端根据文件名或演员名称进行搜索。你可能会将它们写成独立的函数，但在 SQL 中，很容易在一个语句中表达这种选择。当然，你知道 `*count`

```c
int pg_title_search(char *title_to_find, char *name_to_find, int *result_ids[], int *count) {
  int result_size = 0;
  int results = NULL;
  if (title_to_find == NULL && strcmp(title_text, "%*") == 0)
    sprintf(title_text, "%s%%s", title_to_find, "%*");
  else if (name_to_find == NULL && strcmp(actor1, "%*") == 0)
    sprintf(actor1, "%s%%s", name_to_find, "%*");
  exec sql BEGIN WORK;
  exec sql DECLARE mycursor CURSOR FOR SELECT title_id FROM title WHERE
  (title_text LIKE :title_text) AND (actor1 LIKE :actor1) OR
  (actor2 LIKE :actor1)) ORDER BY title_text, actor1, actor2;
  exec sql OPEN mycursor;
```

## 第4章

```c
if (sqlca.sqlcode < 0) {
    pg_print_debug(__FILE__, __LINE__, sqlca, "mycursor");
    exec sql ROLLBACK WORK;
    return DVD_ERR_BAD_TABLE;
}
exec sql FETCH NEXT in mysql INTO :title_id;
while (sqlca.sqlcode == 0) {
    result_size++;
    results = (int*)realloc(results, sizeof(int) * result_size);
    if (results == NULL) /* Major error, don't attempt a recovery */
        exec sql ROLLBACK WORK;
        return DVD_ERR_NO_MEMORY;
    }
    results[result_size - 1] = title_id;
}
exec sql FETCH NEXT in mysql INTO :title_id;
while (sqlca.sqlcode < 0) {
    pg_print_debug(__FILE__, __LINE__, sqlca, "mycursor");
    exec sql ROLLBACK WORK;
    return DVD_ERR_BAD_TABLE;
}
exec sql COMMIT WORK;
*result_ids = results;
*count = result_size;
return DVD_SUCCESS;
}
/* pg_title_search */
```
