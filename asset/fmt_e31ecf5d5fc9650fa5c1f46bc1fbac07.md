
```cpp
enum ePermissions XPCStat::getOwnerPermissions(){
    // 将 st_mode 与 S_IRWX 进行逻辑与运算，提取所有者权限。
    // 返回适当的值。

    switch(sStatBuf.st_mode & S_IRWX)
    {
        case 0:
            return NONE;
        case S_IRWX:
            return READ_WRITE_EXECUTE;
        case S_IRUSR | S_IWUSR:
            return READ_WRITE;
        case S_IRUSR | S_IXUSR:
            return READ_EXECUTE;
        case S_IRUSR:
            return READ;
    }
}
```

```cpp
enum ePermissions XPCStat::getGroupPermissions(){
    // 将 st_mode 与 S_IRWX 进行逻辑与运算，提取组权限。
    // 返回适当的值。

    switch(sStatBuf.st_mode & S_IRWX)
    {
        case 0:
            return NONE;
        case S_IRWX:
            return READ_WRITE_EXECUTE;
        case S_IRGRP | S_IWGRP:
            return READ_WRITE;
        case S_IRGRP | S_IXGRP:
            return READ_EXECUTE;
        case S_IRGRP:
            return READ;
    }
}

enum ePermissions XPCStat::getOtherPermissions(){
    // 将 st_mode 与 S_IRWX 进行逻辑与运算，提取其它权限。
    // 返回适当的值。

    switch(sStatBuf.st_mode & S_IRWX)
    {
        case 0:
            return NONE;
        case S_IRWX:
            return READ_WRITE_EXECUTE;
        case S_IROTH | S_IWOTH:
            return READ_WRITE;
        case S_IROTH | S_IXOTH:
            return READ_EXECUTE;
        case S_IROTH:
            return READ;
    }
}
```

为了避免处理不可访问的文件或目录，你必须知道可以使用哪些文件权限。`cCheckReadAccess()`、`cCheckWriteAccess()` 和 `cCheckExecuteAccess()` 返回应用程序对路径的访问权限。为了检查适当的权利，应用程序需要知道它是否拥有所有者或组权限。在 UNIX 系统中，应用程序可以在运行时假设运行用户不同的所有者或组 ID。运行时假设的 ID 是有效 ID。要确定应用程序是否有所有或组 ID，需要检查真实用户 ID 和有效用户 ID。使用这四个系统调用可以完成此任务。

### 表 2.5

| 类型 | 目的 |
|---|---|
| `unsigned short getuid()` | 返回应用程序正在使用的真实用户 ID。 |
| `unsigned short getgid()` | 返回应用程序正在使用的真实组 ID。 |
| `unsigned short getuid()` | 返回应用程序正在使用的有效用户 ID。 |
| `unsigned short getgid()` | 返回应用程序正在使用的有效组 ID。 |

### 列表 2.6 回答访问问题 29

```cpp
char XPCFileStat::cCheckReadAccess(){
    // 检查我们是否是路径的所有者，或者我们是否拥有有效的
    // 所有 ID。
    if ((StatBuf.st_uid == getuid()) || (sStatBuf.st_uid == getuid())) {
        // 我们是所有者。获取所有者的权限并检查我们是否有
        // 读取权限。如果有读取权限则返回 TRUE，否则返回
        return FALSE;
    }
    enum ePermissions eOwnerPermissions = iGetOwnerPermissions();
    if ((eOwnerPermissions == READ) || (eOwnerPermissions == READ_EXECUTE) ||
        (eOwnerPermissions == READ_WRITE) ||
        (eOwnerPermissions == READ_WRITE_EXECUTE)) {
        return 1;
    } else {
        return 0;
    }
    // 检查我们是否与路径属于同一组，或者我们是否拥有
    // 有效组 ID。
    else if ((StatBuf.st_gid == getgid()) || (sStatBuf.st_gid == getgid())) {
        // 我们与路径属于同一组。检查我们是否有
        // 读取权限。如果有读取权限则返回 TRUE，否则返回
        return FALSE;
    }
    enum eGroupPermissions = iGetGroupPermissions();
    if ((eGroupPermissions == READ) || (eGroupPermissions == READ_EXECUTE) ||
        (eGroupPermissions == READ_WRITE) ||
        (eGroupPermissions == READ_WRITE_EXECUTE)) {
        return 1;
    } else {
        return 0;
    }
    // 如果我们既不是所有者，也不是所有者的组员，则检查
    // 所有其他用户的权限。如果有读取权限则返回
    // TRUE，否则返回 FALSE；
```

## 第 2 章：UNIX 构建块

```cpp
enum ePermissions eOtherPermissions = iGetOtherPermissions();
if ((eOtherPermissions == READ) || (eOtherPermissions == READ_EXECUTE) ||
    (eOtherPermissions == READ_WRITE) ||
    (eOtherPermissions == READ_WRITE_EXECUTE))
    return 1;
else
    return 0;
```

## 将 XPCFileStat 发挥于此

目录遍历程序是一种利用 `XPCFileStat` 提取路径的统计信息和访问权限的应用程序。一个良好的目录遍历程序应该执行以下功能：

- 接受目录树中的起始点，无论是根目录还是子目录。

- 打印它遇到的每个路径的节点，具体包括其名称、类型、大小和权限。

- 确定当前目录下的子目录是否可以被访问，如果是，则遍历它们。

为了遍历目录，需要引入几个新的系统调用。这些系统调用打开目录结构（`opendir()`），读取其内容（`readdir()`），并关闭目录结构（`closedir()`）。所有与目录相关的系统调用原型都在 `dirent.h` 头文件中定义。

## The `opendir()` 系统调用

`opendir()` 函数打开一个与给定路径对应的目录流。打开时，目录流被置于第一个条目。如果目录成功打开，则返回一个指向 `DIR` 类型对象的指针；否则，返回一个空指针。`DIR` 指针用于读取已打开目录的内容。`opendir` 的原型如下：

```c
DIR *opendir(const char *dirname);
```

## The `closedir()` 系统调用
