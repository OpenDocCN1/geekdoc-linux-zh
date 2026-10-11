
如果软件包安装并运行正常，请将你的源码 RPM 上传到你常用的软件仓库，然后就大功告成了。

如果，令人遗憾地，你遇到了问题，RPM 的 build 命令接受几个选项，这些选项允许你逐步执行构建过程，以便识别并（希望）修复问题。以下列表简要描述了这些选项：

- `-bp`—验证 spec 文件的**prep** 部分
- `-bl`—验证 `%files` 中的文件列表
- `-bc`—执行**prep** 和**compile**
- `-bi`—执行**prep**、**compile** 和**install**
- `-bb`—执行**prep**、**compile**、**install**，并且仅构建**build**二进制包
- `--short-circuit`—添加此参数可直接跳到指定的构建步骤（`p`、`l`、`c`、`i`、`b`）
- `--keep-temp`—保留构建过程中创建的临时文件和脚本
- `--test`—执行模拟构建以查看将要执行的操作（也会执行 `--keep-temp`）

在解决错误后，使用 `-ba` 重新构建，上传你的杰作，然后等待赞誉（以及补丁和错误修复）纷至沓来。

# 接下来是什么？

在本章中，你查看了两种不同的软件分发方式：一种是使用 tar、gzip 和 install，另一种是使用 Red Hat Package Manager。这标志着本书的结束。你已学会如何编译程序，涵盖了许多系统编程主题，接触了许多应用程序接口，并简要介绍了网络编程这一庞大领域。你还被介绍了几种基本的编程实用工具，例如 RCS 和 gdd。为了将这些技能融会贯通，下一章将引导你构建一个音乐 CD 数据库。

# 22— 编程项目：音乐 CD 数据库

第 3 章“关于项目”曾带你快速浏览了你在本书末尾完成的编程项目。恭喜！你到了这里！说真的，在前 21 章中你学到了大量关于编程的知识，所以现在该把这些知识付诸实践了。本章将带你通过一个小程序——音乐 CD 数据库——使你学到许多内容变得切实可感（或者至少在一零数字所能表达的范围内可感）。具体而言，本章包含以下内容：

- 音乐 CD 数据库程序的完整源代码。
- 对程序的彻底解释，逐模块说明。
- 关于如何改进和扩展程序的建议。

# 代码，逐模块解析

如第 3 章所述，用户级程序 `mcdcli.c` 和 `mcdui.c` 严重依赖于辅助模块 `mcddb.c`。因此，花些时间研究一下这个辅助模块似乎是合理的，因为它实现了用户程序的大部分功能。我将其称为数据库管理器，因为它处理与底层数据库和 Berkeley 数据库 API 的大部分交互。以下是头文件和源文件：

```c
/*
 * mcddb.h - Database module for Music CD database
 */
#ifndef MCDB_H_
#define MCDB_H_

#include <db.h>

/*
 * Open the database named in dbpath, or, if it is NULL, assume that
 * we want PWD/mcd.db. Return 0 on success, errno or -1 on failure.
 */
int open_db(char *dbpath);

/*
 * Sync and close the currently open database. Always returns 0.
 */
int close_db(void);

/*
 * Add the record with a key of kbuf and a value of vbuf to the
 * currently opened database. Returns 0 on success, 1 if the key
 * already exists, and errno otherwise.
 */
int add_rec(char *kbuf, char *vbuf);

/*
 * Delete the record whose key matches kbuf. On success, syncs the
 * database to disk and returns 0; on failure, returns 1 if a key
 * matching kbuf was not found or errno otherwise.
 */
int del_rec(char *kbuf);

/*
 * Iterate through the database, searching for a key matching kbuf.
 * On success, returns 0 and stores the data corresponding to kbuf
 * in value. On failure, returns DB_NOTFOUND or errno.
 */
int find_rec(char *kbuf, DBT *value);

/*
 * Retrieve the record matching key from the database. Returns 0 on
 * success and stores the corresponding value in value, 1 if the
 * indicated key is not found, and errno otherwise.
 */
int get_rec(char *kbuf, DBT *value);

/*
 * Count the number of records in the database by iterating through it
 * with a cursor. Returns the number of records if successful or 0 if
 * the database is empty or an error occurs.
 */
int count_recs(void);

/*
 * Iterate through the entire database, listing each record consecutively
 * and alphabetically by key. Returns number of records stored in kbuf and
 * vbuf on success. Returns 0 if no records available. On failure, returns
 * errno.
 */
int list_recs(char **keys, char **values);

#endif /* MCDB_H_ */
```

`#ifdef/#endif` 条件保护头文件免受多次包含的影响，这会导致 `gcc` 发出关于变量或函数被重新定义的警告或错误。该头文件声明了用于打开和关闭数据库的函数，以及用于访问和操作数据库中记录的各种函数。

当前定义的接口有一个缺点，即它假设访问的是 Berkeley db 数据库。`find_rec` 和 `get_rec` 函数期望一个指向 DBT 结构的指针；这种依赖可以通过将这些参数改为简单的字符字符串指针来解决。

接下来是数据库管理器的实现：

```c
/*
 * mcddb.c - Database manager for music CD database
 */
#include <db.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include "mcddb.h"

static DB *db;          /* Global database pointer */

int open_db(char *dbpath)
{
    int ret;
    char *defpath = "./mcd.db";

    /*If dbpath is NULL, assume the current dir name the DB mcd.db */
    if(!dbpath) {
        if ((dbpath = malloc(strlen(defpath) +1)) != NULL) {
            strcpy(dbpath, defpath);
        } else {
            return -1;
        }
    }

    ret = db_open(dbpath, DB_BTREE, DB_CREATE, 0600, NULL, NULL, &db);
    if(ret != 0) {
        return ret; /* Fatal */
    }
    return 0;
}

int close_db(void)
{
    /* db->close should force a sync, but just in case */
    db->sync(db, 0);
    db->close(db, 0);
    return 0;
}

int add_rec(char *kbuf, char *vbuf)
{
    DBT key, value;
    int ret;

    /* Initialize the DBTs */
    memset(&key, 0, sizeof(DBT));
    memset(&value, 0, sizeof(DBT));

    /* This looks perverse, but it works */
    key.data = kbuf;
    key.size = strlen(kbuf);
    value.data = vbuf;
    value.size = strlen(vbuf);

    /* Store the record */
    ret = db->put(db, NULL, &key, &value, DB_NOOVERWRITE);
    if(ret == DB_KEYEXIST) /* Key already exists */
        return 1;
    else if(ret != 0) /* Some other error occurred */
        return ret;
    /* Sync the database */
    db->sync(db, 0);
    return 0; /* Success! */
}

int del_rec(char *kbuf)
{
    int ret;
    DBT key;
    memset(&key, 0, sizeof(DBT));
    key.data = kbuf;
    key.size = strlen(kbuf);

    ret = db->del(db, NULL, &key, 0);
    if(ret != 0) {
        if (ret == DB_NOTFOUND) { /* Key not found */
            return 1;
        } else {
            return ret;
        }
    }
    /* Sync the database */
    db->sync(db, 0);
    return 0;
}

int find_rec(char *kbuf, DBT *value)
{
    int ret;
    DBT key; /* Copy kbuf here */
    DBC *dbc = NULL; /* A database cursor */

    /* Create the cursor */
    ret = db->cursor(db, NULL, &dbc);
    if (ret != 0) { /* Something went wrong */
        return ret;
    }

    /* Initialize DBT key; assume 'value' is already init'ed */
    memset (&key, 0, sizeof(DBT));
    key.data = kbuf;
    key.size = strlen(kbuf);

    /* Iterate through the database, looking for a match */
    while((ret = dbc->c_get(dbc, &key, value, DB_NEXT)) != DB_NOTFOUND) {
        /*
         * This is tricky, db does not store null-terminated strings,
         * so use strncmp to limit the bytes compared to the length
         * of the search string. To make sure the match is legitimate,
         * compare the length of the search string to key.size. If they
         * are equal, assume the match is good.
         */
        if(!strncmp(key.data, kbuf, strlen(kbuf))) {
            if(key.size == strlen(kbuf)) { /* Found a match */
                break;
            }
        }
    }
    /* Did we fall through or find a match? */
    if(ret == DB_NOTFOUND) {
        return 1;
    }
    return 0;    /* Happy, happy, joy, joy */
}

int get_rec(char *kbuf, DBT *value)
{
    int ret;
    DBT key;

    /* Initialize the key DBT; assume value init'ed by caller */
    memset(&key, 0, sizeof(DBT));
    key.data = kbuf;
    key.size = strlen(kbuf);

    /* See if we can get the record */
    ret = db->get(db, NULL, &key, value, 0);
    switch(ret) {
        case 0:        /* Bliss */
            return 0;
        case DB_NOTFOUND:        /* Key not found */
            return 1;
        default:        /* Unknown error */
            return ret;
    } /* end switch */
}
```

