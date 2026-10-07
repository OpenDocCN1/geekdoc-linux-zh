
```cpp
1: // stat.cc
2:
3: #include <iostream>
4: #include <string.h>
5: #include <errno.h>
6: #include <sys/types.h>
7: #include <sys/stat.h>
8:
9:
10: /////////////////////////////////////////////////////////
11: // Simple Stat 对象：
12: /////////////////////////////////////////////////////////
13:
14: class Stat : public stat {
15:
16: private:
17:     char *path;            // 路径名
18:     int fd;               // 文件描述符
19:
20: public:
21:     Stat() { path = 0; fd = -1; }
22:     ~Stat();
23:
24:     Stat & examine(const char *pathname);
25:     Stat & examine(int fd);
26:     int operator=(Stat &o);
27:
28:     friend ostream & operator<<(ostream&out, Stat &o);
29: };
30:
31: /////////////////////////////////////////////////////////
32: // 析构函数：
33:
34:
35:::~Stat() {
36:     if ( path )             // 路径已分配
37:         delete path;      // 是，释放字符串
38: }
39:
40: /////////////////////////////////////////////////////////
41: // 基于路径名的 stat(2) ：
42: /////////////////////////////////////////////////////////
43:
44: Stat &
45: Stat::examine(const char *pathname) {
46:
47:     if ( path )           // 路径已分配
48:         delete path;      // 是，释放字符串
49:     path = strdup(pathname); // 创建新字符串
50:     fd = -1;               // 标记为不存在
51: }
52:
53: /////////////////////////////////////////////////////////
54: /////////////////////////////////////////////////////////
55: // 基于文件描述符的 fstat(2) ：
56: /////////////////////////////////////////////////////////
57:
58: Stat &
59: Stat::examine(int fd) {
60:
61:     if ( path )           // 路径已分配
62:         delete path;      // 是，释放字符串
63:     path = 0;
64:     fd = fd;               // 保存 fd
65: }
66:
67: /////////////////////////////////////////////////////////
68: /////////////////////////////////////////////////////////
69: // 运算符重载：
70: ostream &operator<<(ostream&out, Stat &o) {
71:     // 如果没有信息
72:     if (fd == -1 && path) {
73:         out << "没有信息。";
74:         return out;
75:     }
76:     // 否则，显示 stat 信息
77:     if (path) {
78:         out << "st_dev: " << o.st_dev << "\n";
79:         out << "st_ino: " << o.st_ino << "\n";
80:         out << "st_mode: " << o.st_mode << "\n";
81:         out << "st_nlink: " << o.st_nlink << "\n";
82:         out << "st_uid: " << o.st_uid << "\n";
83:         out << "st_gid: " << o.st_gid << "\n";
84:         out << "st_rdev: " << o.st_rdev << "\n";
85:         out << "st_atime: " << o.st_atime << "\n";
86:         out << "st_atnsec: " << o.st_atnsec << "\n";
87:         out << "st_mtime: " << o.st_mtime << "\n";
88:         out << "st_mtimsec: " << o.st_mtimsec << "\n";
89:         out << "st_ctime: " << o.st_ctime << "\n";
90:         out << "st_ctimsec: " << o.st_ctimsec << "\n";
91:         out << "st_size: " << o.st_size << "\n";
92:         out << "st_blocks: " << o.st_blocks << "\n";
93:         out << "st_blksize: " << o.st_blksize << "\n";
94:         out << "st_flags: " << o.st_flags << "\n";
95:         out << "st_gen: " << o.st_gen << "\n";
96:     }
97:     return out;
98: }
99:
100: /////////////////////////////////////////////////////////
101: // 此方法测试两个文件系统对象
102: // 是否为同一个：
103: /////////////////////////////////////////////////////////
104: int
105: Stat::operator==(Stat &o) {
106:     // 是否任一个对象缺少信息？
107:     if (fd == -1 && path) {
108:         throw EINVAL;      // 这里没有信息
109:     }
110:     if (o.fd == -1 && !path) {
111:         throw EINVAL;      // 那里没有信息
112:     }
113:
114:     // 现在测试这些是否是同一个对象：
115:     if (o.st_dev != st_dev)                           // 设备匹配吗？
116:         || o.st_ino != st_ino)                            // inode 匹配吗？
117:         return 0;
118:     }                                                 // 设备或 inode 不匹配
119:
120:     return 1;                                         // 返回 TRUE，它们是同一个
121: }
122:
123: /////////////////////////////////////////////////////////
124: // 测试主程序：////////////////////////////////////////////////////////////////
125: //////////////////////////////////////////////////////////////////
126:
127: int
128: main(int argc, char **argv) {                      // 工作索引
129:     int x;
130:     Stat t;                                             // stat("./stat")
131:     t.examine("./stat");                             // 使用路径名 stat
132:     cout << t;                                     // 输出 stat 信息
133:     x = open("./stat", O_RDONLY);                   // 打开
134:     t.examine(x);                                  // fstat
135:     cout << t;                                     // 输出 fstat 信息
136:     close(x);
137:     return 0;
138: }
```

## 第 6 章 • 管理文件及其属性 115

```cpp
159:   Stat s;                      // 工作 stat 对象
160:   t.examine(".stat");         // 执行 stat(2)
161: 
162:
163:   // 现在尝试命令行参数：
164:
165:   for (int x=1; x<argc; ++x) {
166:
167:      try {
168:          s.examine(argv[x]);      // Stat 此路径名
169:      } catch (int e) {
170:          // e 是 errno 值：
171:          cerr << strerror(e) << ": " << stat(2) << "; ";
172:
173:          argv[x] << '\n';
174:
175:          continue;
176:
177:      cout << s << '\n';        // 打印 stat 信息
178:
179:   } // 测试 s 是否与 t 相同：
180:
181:      cout << "* " << argv[x] << " is "
182:           << (s == t ? "same" : "not the same")
183:
184:           << " file as ./stat\n";
185:
186:      return 0;
187:   }
188:
//   // End stat.cc
```

列表 6.1 中的程序从第 14 行开始定义了 `Stat` 类。该类继承自 `stat` 结构体，并为了简单起见暴露了 `stat` 成员（注意第 14 行中的 `public` 关键字）。第 17 和 18 行声明了两个私有成员 `path` 和 `fd` 用于跟踪。

第 24 和 25 行定义了两个 C++ 方法，允许对象通过路径名或文件描述符进行查询。这最终会转换为对 `stat(2)` 或 `fstat(2)` 的调用。

第 45–82 行声明了通过路径名查询的实现。第 54 行显示了对 `stat(2)` 的调用。注意，该方法的设计是在如果 `stat(2)` 返回错误则抛出 `errno` 值。第 64–79 行同样定义了通过文件描述符查询的实现。`fstat(2)` 调用出现在第 75 行，同样，如果返回错误则会显示 `errno`。

第 86–125 行定义了一个友函数（第 28 行），允许将 `Stat` 类及其 `stat` 成员发送到 `cout`。

`main()` 程序中第 165–188 行的循环对命令行提供的每个路径名进行解析（第 168 行）。任何错误在第 169 行被捕获并在第 171–173 行报告。如果 `s.examine(argv[x])` 执行成功，控制将传递到第 176 行，在那里对其内容进行格式化输出。

以下会话显示了使用 `Makefile` 文件编译并测试列表 6.1 中的程序：

```bash
$ make stat
cc -C -D_POSIX_C_SOURCE=199309L -Wall -handle-exceptions stat.cc
cc stat.0 -o stat -lstatcc
./stat
stat(Makefile) {
    st_dev = 196613;
    st_ino = 125953;
    st_mode = 0100644;
    st_nlink = 1;
    st_uid = 1001;
    st_gid = 1001;
    st_rdv = 525400;
    st_atime = 956799796;
    st_mtime = 956723168;
    st_ctime = 956723168;
    st_size = 378;
    st_blocks = 2;
    st_blksize = 8192;
    st_flags = 0;
    st_gen = 0;
}
'Makefile' is not the same file as ./stat
```

注意，如果我们验证文件的几个属性，它们将与显示的输出一致：

```bash
$ ls -li Makefile
125953 -rw-r--r--  user group 378 Apr 26 Makefile
```

378 字节的文件大小与 `st_size` 显示的值匹配，权限 `rw-r--r--` 与 `st_mode` 位的最后八进制数字匹配。`ls(1)` 的 `-i` 选项允许显示 inode。它显示为 `125953` 并与 `st_ino` 值一致。

### 针对同一文件的链接测试

当两个不同名称的 `st_dev` 中的设备和 `st_ino` 中的 inode 匹配时，表明它们是指向同一个文件的链接。列表 6.1 中的 `Stat` 类中定义了 `operator==` 方法，允许使用 `Stat` 对象进行比较。该方法在第 132–149 行实现。

在 `main()` 程序中，该方法通过通过最初获取可执行文件的 `stat(2` 来 来测试。然后于第 181 行对命令行参数进行比较（注意 `==` 运算符）。在早前的测试运行中，显示了信息 `'Makefile' is not the same file as ./stat`。然而，如果使用链接到 `./stat` 的 `link_link` 测试此程序，则得到了以下结果：

```bash
$ ln ./stat link_link
$ ./stat link_link
stat(link_link) {
  st_dev = 196613;
  st_ino = 125953;
  st_mode = 0100755;
  st_nlink = 2;
  st_uid = 1001;
  st_gid = 1001;
  st_rdv = 525400;
  st_atime = 956799796;
  st_mtime = 956723168;
  st_ctime = 956723168;
  st_size = 378;
  st_blocks = 2;
  st_blksize = 8192;
  st_flags = 0;
  st_gen = 0;
}
'link_link' is same file as ./stat
$ ls -li link_link
125953 -rwxr-xr-x  user group 378 Apr 26 link_link
```

在创建到 `./stat` 的链接后，程序正确指出路径名 `link_link` 与 `./stat` 是相同文件。这在 `main()` 程序的第 180–182 行。

### 测试类型

`st_mode` 也包含文件类型信息。要确定对象类型，使用以下宏之一，其中 `m` 是要测试的 `st_mode` 值。可以使用以下测试和宏：

| | |

| :--- | :--- |

| 符号链接 | `S_ISNK(m)` |

| 普通文件 | `S_ISREG(m)` |

| 目录 | `S_ISDIR(m)` |

| 字符特殊设备 | `S_ISCHR(m)` |

| 块特殊设备 | `S_ISBLK(m)` |

| 命名管道 (FIFO) | `S_ISFIFO(m)` |

| 套接字 | `S_ISSOCK(m)` |

这些宏测试 `stat` 结构体中的 `st_mode` 高位。以下代码显示了函数如何报告作为参数的文件系统对象类型：
