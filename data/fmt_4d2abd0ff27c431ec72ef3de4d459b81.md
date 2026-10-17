
```cpp
6:    #include <sys/types.h>

7:    #include <unistd.h>

8:    #include <ndbm.h>

9:    #include <fcntl.h>

10:

11:   ///////////////////////////////////////////////////////

12:   // 用于 Dbm 的类////////////////////////////////////

13:   ///////////////////////////////////////////////////////

14:

15:   class Dbm {

16:       int     flags;      // 标志
17:       char*path;       // 路径
18:       Dbm*db;        // 数据库
19:   protected:
20:       int     error;      // 错误
21:   public:
22:       Dbm();
23:       ~Dbm();
24:       Dbm &open(const char *path,int flags=O_RDWR,int mode=666);
25:       Dbm &close();
26:       datum fetch(datum key);
27:       Dbm &store(datum key,datum content,int flags);
28:       Dbm &deleteKey(datum key);
29:       datum firstKey();
30:       datum nextKey();
31:       inline int getError() { return error; }
32:       inline int getFlags() { return flags; }
33:       inline char *getPath() { return path; }
34:   };

35:

36: #endif // Dbm_h

37:

38: // Dbm.h 结束
```

`Dbm` 对象管理 `flags`、`path` 和 `db`。可以通过 `getFlags()` 和 `getPath()` 查看标志和路径。受保护成员 `error` 存储 `errno` 值，可以通过 `getError()` 查看。

`open()`、`close()`、`fetch()`、`store()`、`deleteKey()`、`firstKey()` 和 `nextKey()` 是本章学过的各种函数的封装。方法不能命名为 `delete()`，因为它与关键字冲突。

列表 14.4 显示了 `Dbm` 类的实现。

# 列表 14.4 Dbm.cc—Dbm 类的实现

```cpp
1:    // Dbm.cc

2:

3:    #include <string.h>

4:    #include <errno.h>

5:    #include "Dbm.h"

6:

7:    /////////////////////////////////////////////////////

8:    // 构造函数////////////////////////////////////

9:    /////////////////////////////////////////////////////

10:

11:    Dbm::Dbm() {

12:        flags = 0;                  // 标志
13:        path = 0;                   // 路径
14:        db = 0;                     // 数据库
15:        error = 0;                  // 错误
16:    }

17:

18:    /////////////////////////////////////////////////////

19:    // 析构函数////////////////////////////////////

20:    /////////////////////////////////////////////////////

21:

22:    Dbm::~Dbm() {

23:     if ( db )
24:         close();                      // 关闭数据库
25:     }

26: ///////////////////////////////////////////////////
27: // 打开/创建数据库///////////////////////////////
28: // 注意:
29: // // flags                      O_RDWR, O_RDONLY, O_CREAT 等 (见 open(2))
30: // // mode                         权限位
31: ///////////////////////////////////////////////////

33:     Dbm &&
34:     Dbm::open(const char *path,int flags,int mode) {

36:         if ( db )
37:             throw error = EPERM;      // 数据库已打开

39:             db = dbm_open(path,this->flags = flags,mode);
40:             if (! db )
41:                 throw error = EIO;       // 打开失败

43:             path = strdup(path);      // 保存路径

45:             return *this;
46:     }
47: ///////////////////////////////////////////////////////////////////
48: // 关闭打开的数据库 :
49: ///////////////////////////////////////////////////////////////////

51:     Dbm &&
52:     Dbm::close() {

54:         if (! db )
55:             throw error = EPERM;      // 数据库未打开

57:             dbm_close(db);            // 关闭数据库
58:             db = 0;
59:             delete path;              // 释放路径
60:             path = 0;

62:         return *this;
63:     }

65: ///////////////////////////////////////////////////////////////////
66: // // 通过键获取数据 : EIO;
67: ///////////////////////////////////////////////////////////////////

69:     datum
70:     Dbm::fetch(datum key) {
71:         datum content;

73:         if (! db )
```

# 286 高级 UNIX 编程

接上页

```cpp
76:   throw error = EPERM; // 没有数据库
77:   content = ::dbm_fetch(db,key);
78:   if ( dbm_error(db) ) {
79:     dbm_clearerr(db);
80:     throw error = EIO;
81:   }
82:   }
83:   if (!content.dptr) // 未找到
84:     throw error = ENOENT;

86:   return content; // 找到内容
87: }
```

```cpp
////////////////////////////////////////////////////////////////////////
90: // 通过键替换或插入新数据：
92: 
```

```cpp
93: Dbm &
94: Dbm::store(datum key,datum content,int flags) {

96:   if (db )
97:     throw error = EPERM; // 没有数据库

99:   if (:dbm_store(db,key,content,flags) < 0 ) {
100:    dbm_clearerr(db);
101:    throw error = EIO; // 失败
102:  }
103:  return *this;
104: }
```

```cpp
////////////////////////////////////////////////////////////////////////
107: // 通过键删除数据：
109: 
```

```cpp
110: Dbm &
111: Dbm::deleteKey(datum key) {

113:   if (db )
114:     throw error = EPERM; // 没有数据库
115:   if (:dbm_delete(db,key) < 0 ) {
116:     dbm_clearerr(db);
117:     throw error = EIO; // 失败
118:   }
119:   return *this;
120: }
```

```cpp
////////////////////////////////////////////////////////////////////////
123: // 获取第一个数据键：
125: 
```

```cpp
126: datum
127: Dbm::firstKey() {
```

# 第 14 章 • 数据库库例 287

```cpp
128:  datum d;

130:  if ( db )
131:      throw error = EPERM;      // 没有数据库

133:  d = ::dbm_firstkey(db);

135:  if ( dbm_error(db) ) {
136:      dbm_clearerr(db);
137:      throw error = EIO;      // 数据库错误
138:  }

140:  return d;
141:  }

143: ///////////////////////////////////////////////////////////////////
144: // 获取下一个数据键：
145: ///////////////////////////////////////////////////////////////////

147:  datum
148:  Dbm::nextKey() {
149:      datum d;

151:      if ( db )
152:          throw error = EPERM;      // 没有数据库

154:      d = ::dbm_nextkey(db);

156:      if ( dbm_error(db) ) {
157:          dbm_clearerr(db);
158:          throw error = EIO;      // 数据库错误
159:      }

161:      return d;
162:  }

164: // 结束 Dbm.cc
```

列表 14.4 中的析构函数 `Dbm::~Dbm()` 在发现私有成员不为空时会调用 `Dbm::close()`。这允许数据库在 `Dbm` 对象被销毁时自动关闭。然而，用户也可以也可以手动调用 `Dbm::close()`。这允许他通过调用 `Dbm::open()` 打开另一个数据库来重用该对象。

`Dbm::fetch()`、`Dbm::store()`、`Dbm::deleteKey()`、`Dbm::firstKey()` 和 `Dbm::nextKey()` 方法使用数据类型的方式与 `ndbm(3)` 例程相同。`Inode` 类将为应用程序定制接口，你将在本章随后的列表中看到这些。

与 `Dir` 类的实现类似，当数据库未打开且尝试进行操作时，`Dbm` 类会抛出错误 `EPERM`。与 `Dir` 类不同，在 `ndbm(3)` 失败后抛出的错误始终是 `EIO`。这样做是因为 `ndbm(3)` 例程没有提供记录在案的错误。文献表明，只有 `dbm_error(3)` 是可信的，而且它仅仅是一个错误指示。`errno` 的值在不同的 UNIX 平台上返回得并不一致。`Dbm::fetch()` 方法在第 79-82 行展示了这一点。

其余实现提供了 `ndbm(3)` 例程的封装。

# Inode 类

`Dbm` 类是一个基础类。数据库使用设备号和 inode 号作为每条记录的键。此外，每条记录仅仅是 `struct` 数据。继承自 `Dbm` 类的新类可以为应用程序提供方便的接口。这就是列表 14.5 所示的 `Inode` 类的工作。

## 列表 14.5 Inode.h—Inode 类

```cpp
1: // Inode.h
2:
3: #ifndef _INODE_H
4: #define _INODE_H
5:
6: #include <sys/types.h>
7: #include <sys/stat.h>
8: #include <dbm.h>
9:
10: ///////////////////////////////////////////////////
11: // 用于 Inode 数据库的专用数据库类
12: ///////////////////////////////////////////////////
13:
14: class Inode : public Dbm {
15: public:
16:     struct Key {
17:         dev_t st_dev;               // 设备号
18:         ino_t st_ino;              // inode 号
19: };
20: protected:
21:     Key key;                       // 内部键
22: public:
23:     Inode& fetchKey(Key key, struct stat &sbuf)
24:     Inode& insertKey(Key key, struct stat &sbuf)
25:     Inode& replaceKey(Key key, struct stat &sbuf)
26:     Inode& deleteKey(Key key);
27:     Key *firstKey();
28:     Key *nextKey();
29: };
30:
31: #endif // _INODE_H
32:
33: // 结束 Inode.h
```

列表 14.5 显示了 `Inode` 类如何继承 `Dbm` 类。`Inode::Key` 的定义在第 15-19 行公开。保护内部键成员在第 21 行声明。

第 23-28 行实现了对应用程序方便的 API。在每个情况下，键都使用 `Inode::Key` 类型。如果涉及数据，则引用 `struct stat`。

`Inode` 类的实现见列表 14.6。

## 列表 14.6 Inode.cc—Inode.cc 的实现

```cpp
1: // Inode.cc
2:
3: #include <errno.h>
4: #include "Inode.h"
5:
6: ///////////////////////////////////////////////////
7: // 通过 inode 号获取 stat 信息
8: ///////////////////////////////////////////////////
9:
10: Inode &
11: Inode::fetchKey(Key key, struct stat &sbuf) {
12:     datum f;

14:     f.dptr = (char *)&key;
15:     f.dsize = sizeof(key);
16:     f = fetch;
```
