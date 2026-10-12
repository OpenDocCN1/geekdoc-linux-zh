devices. The storage parameters specify how the tablespace is used. They are very important and will be discussed in greater detail later in this chapter.

Creating tablespaces is done with the CREATE TABLESPACE command using various options. Not every option will be covered here, since there are so many of them, and since you can easily look them up, but let’s look at a few of The basic commands to create a tablespace are

```
CREATE [UNDO] TABLESPACE *tname*
*DATAFILE data_file_name data_file_size*
*[storage clause]*
*[BLOCKSIZE size [K]]*
*[TEMPORARY]*
*[EXTENT MANAGEMENT DICTIONARY]*
*[EXTENT MANAGEMENT LOCAL [AUTOALLOCATE]]*
*[EXTENT MANAGEMENT LOCAL [UNIFORM SIZE *size* [K,M]]*
*[SEGMENT SPACE MANAGEMENT AUTO]*
*[SEGMENT SPACE MANAGEMENT MANUAL]*
```

Let’s look at these key parameters in a little more detail.

| Parameter | Use |
| :--- | :--- |
| UNDO | The undo parameter specifies that the tablespace you are creating is an undo tablespace. Undo tablespaces are covered in detail in the next chapter. |
| Storage clause | The storage clause specifies the filename, size, and so on. |
| BLOCKSIZE | The BLOCKSIZE parameter is used to allow you to create a nonstandard block size tablespace. |
| TEMPORARY | Specifies that the tablespace is used as a temporary tablespace. |
| EXTENT MANAGEMENT | The EXTENT MANAGEMENT clause allows you to specify whether the tablespace is locally or dictionary managed. |
| SEGMENT SPACE MANAGEMENT | The SEGMENT SPACE MANAGEMENT clause is used to specify AUTOMATIC (bitmap) or MANUAL (freelist) management of free space within segments. |

There are many more optional parameters that can be used to create tablespaces. These optional parameters can be found in the Oracle documentation. Here are a few examples of creating tablespaces.

A locally managed simple tablespace

```
CREATE TABLESPACE *ts1*
*DATAFILE ‘/u01/app/oracle/oradata/orac/ta01.dbf’ SIZE 10M;*
```