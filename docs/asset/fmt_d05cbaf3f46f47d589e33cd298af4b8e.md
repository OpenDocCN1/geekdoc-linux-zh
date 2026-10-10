
```c
static int command_mode(int argc, char *argv[])
{
    int c;
    int result = EXIT_SUCCESS;
    char *prog_name = argv[0];

    /* getopt 使用的外部变量 */
    extern char *optarg;
    extern int optind;

    while ((c = getopt(argc, argv, ":i")) != -1) {
        switch(c) {
            case 'i':
                if (!database_initialize(1)) {
                    result = EXIT_FAILURE;
                    fprintf(stderr, "Failed to initialize database\n");
                }
                break;
            case ':':
            case '?':
            default:
                fprintf(stderr, "Usage: %s [-i]\n\n", prog_name);
                result = EXIT_FAILURE;
                break;
        } /* switch */
    } /* while */
    return(result);
}
```

# 尝试一下—`cd_access.c`

现在我们来看访问`dbm`数据库的函数。

- 1. 往常一样，我们从一些`#include`文件开始。然后我们使用一些`#define`来指定用于存储数据的文件。

- 2. 我们使用两个文件变量来跟踪当前数据库：

```c
static DBM *cdc_dbm_ptr = NULL;
static DBM *cdt_dbm_ptr = NULL;
```

- 3. 默认情况下，`database_initialize`函数打开一个已存在的数据库，但通过非零（即真）参数`new_database`，我们可以强制它创建一个新的（空的）数据库，从而移除任何已存在的数据库。如果数据库初始化成功，两个数据库指针也会被初始化，表示数据库已打开。

```c
int database_initialize(int new_database)
{
    int open_mode = O_CREAT | O_RDWR;

    /* 如果任何数据库已打开，则关闭它 */
    if (cdc_dbm_ptr) dbm_close(cdc_dbm_ptr);
    if (cdt_dbm_ptr) dbm_close(cdt_dbm_ptr);

    if (new_database) {
        /* 删除旧文件 */
        unlink(CDC_FILE_BASE);
        unlink(CDC_FILE_DIR);
        unlink(CDT_FILE_BASE);
        unlink(CDT_FILE_DIR);
    }

    /* 如果需要，打开一些文件 */
    cdc_dbm_ptr = dbm_open(CDC_FILE_BASE, open_mode, 0644);
    cdt_dbm_ptr = dbm_open(CDT_FILE_BASE, open_mode, 0644);
    if (!cdc_dbm_ptr || !cdt_dbm_ptr) {
        fprintf(stderr, "Unable to create database\n");
        cdc_dbm_ptr = cdt_dbm_ptr = NULL;
        return (0);
    }
    return (1);
}
```

- 4. 如果数据库已打开，`database_close`简单地关闭数据库并将两个指针置空。

```c
void database_close(void)
{
    if (cdc_dbm_ptr) dbm_close(cdc_dbm_ptr);
    if (cdt_dbm_ptr) dbm_close(cdt_dbm_ptr);

    cdc_dbm_ptr = cdt_dbm_ptr = NULL;
}
```

- 5. 接下来，有一个函数在传入目录字符串时检索单个目录条目。如果未找到条目，返回的数据字段将为空。

```c
cdt_entry get_cdc_entry(const char *catalog_ptr)
{
    cdt_entry entry_to_return;
    char entry_to_find[CAT_CAT_LEN + 1];
    datum local_data_datum;
    datum local_key_datum;
    memset(entry_to_return, '\0', sizeof(entry_to_return));

    if (!cdc_dbm_ptr || !cdt_dbm_ptr) return (entry_to_return);
    if (!catalog_ptr) return (entry_to_return);
    if (strlen(catalog_ptr) > CAT_CAT_LEN) return (entry_to_return);
    memset(entry_to_find, '\0', sizeof(entry_to_find));
    strcpy(entry_to_find, catalog_ptr);
```

- 6. 我们首先进行合法检查，确保数据库已打开且传入的参数是合理的——即键包含有效的字符串。

- 7. 我们先设置数据库结构，然后使用`dbm_fetch`获取数据。如果没有检索到数据，我们返回初始化的`entry_to_return`结构。

```c
local_key_datum.dptr = (void *) entry_to_find;
local_key_datum.dsize = sizeof(entry_to_find);

memset(local_data_datum, '\0', sizeof(local_data_datum));
local_data_datum = dbm_fetch(cdc_dbm_ptr, local_key_datum);
if (local_data_datum.dptr) {
    memcpy(&entry_to_return, (char *)local_data_datum.dptr,
        local_data_datum.dsize);
}
    return (entry_to_return);
} /* get_cdc_entry */
```

- 8. 获取单个曲目条目更好，下一个函数以与`get_cdc_entry`相同的方式实现，参数是目录指针和曲目号。
