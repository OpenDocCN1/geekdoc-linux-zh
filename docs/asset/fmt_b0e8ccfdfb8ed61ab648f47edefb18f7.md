
# 292 高级 UNIX 编程

# 列表 14.7 Snapshot.cc—Snapshot 应用程序

```cpp
18:     if ( f.dsize != sizeof(struct stat) )
19:         throw error = EINVAL; // 数据库损坏
20:     memcpy(&sbuf, f.dptr, sizeof(sbuf));
21:
22:     return *this;
23: }
24:
25: ///////////////////////////////////////////////////
26: // 通过 inode 号添加新的 stat 信息
27: ///////////////////////////////////////////////////
28:
29: Inode &
30: Inode::insertKey(Key key, struct stat &sbuf) {
31:     datum k;
32:
33:     k.dptr = (char *)&key;
34:     k.dsize = sizeof(key);
35:     c.dptr = (char *)&sbuf;
36:     c.dsize = sizeof(sbuf);
37:     store(k, c, DBM_INSERT);
38:
39:     return *this;
40: }
```

```cpp
40:
41: ///////////////////////////////////////////////////
42: // 通过 inode 号替换 stat 信息
43: ///////////////////////////////////////////////////
44:
45: Inode &
46: Inode::replaceKey(Key key, struct stat &sbuf) {
47:     datum k, c;
48:
49:     k.dptr = (char *)&key;
50:     k.dsize = sizeof(key);
51:     c.dptr = (char *)&sbuf;
52:     c.dsize = sizeof(sbuf);
53:     store(k, c, DBM_REPLACE);
54:     return *this;
55: }
56:
57: ///////////////////////////////////////////////////////////////////
58: // 通过 inode 号删除 stat 信息
59: ///////////////////////////////////////////////////////////////////
60:
61: Inode &
62: Inode::deleteKey(Key key) {
63:     datum k;
64:
65:     k.dptr = (char *)&key;
66:     k.dsize = sizeof(key);
67:     Dbm::deleteKey(k);
68:     return *this;
69: }
```

```cpp
70:
71: ///////////////////////////////////////////////////////////////////
72: // 获取第一个键：
73: ///////////////////////////////////////////////////////////////////
74:
75: Inode &
76: Inode::firstKey() {
77:     datum d;
78:
79:     if ( db )
80:         throw error = EPERM;      // 没有数据库
81:
82:     d = ::dbm_firstkey(db);
83:
84:     if ( dbm_error(db) ) {
85:         dbm_clearerr(db);
86:         throw error = EIO;      // 数据库错误
87:     }
88:
89:     return d;
90: }
91:
92: ///////////////////////////////////////////////////////////////////
93: // 获取下一个键：
94: ///////////////////////////////////////////////////////////////////
95:
96: Inode &
97: Inode::nextKey() {
98:     datum d;
99:
100:     if ( db )
101:         throw error = EPERM;      // 没有数据库
102:
103:     d = ::dbm_nextkey(db);
104:
105:     if ( dbm_error(db) ) {
106:         dbm_clearerr(db);
107:         throw error = EIO;      // 数据库错误
108:     }
109:
110:     return d;
111: }
112:
113: // 结束 Inode.cc
```

```c
1:  // Snapshot.cc
2: 
3: #include <stdio.h>
4: #include <stdlib.h>
5: #include <unistd.h>
6: #include <errno.h>
7: #include <string.h>
8: #include <sys/types.h>
9: #include <sys/stat.h>
10: #include <pwd.h>
11: #include <grp.h>
12: 
13: #include "Dir.h"
14: #include "InoDb.h"
15: 
16: static int rc = 0; // 返回码
17: static int cmdopt_i = 0; // -i
18: static int cmdopt_c = 0; // -c
19: static int cmdopt_v = 0; // -v
20: static int cmdopt_h = 0; // -h
21: 
22: // 返回路径的基文件名 (BASENAME) ：
23: 
25: char *
26: Basename(char *path) {
27:     char *bname = strchr(path,'/');
28: 
29:     return bname ? bname : bname + 1;
30: }
31: 
32: // 比较当前与之前的 stat(2) 信息 ：
33: 
37: char *
38: Compare(struct stat is,struct stat was) {
39:     static char cmpsg[512]; // 比较消息缓冲区
40:     static char dtbuf[64]; // 日期时间格式缓冲区
41:     struct passwd *pwd = NULL; // 查找 /etc/password
42:     struct group *grp = NULL; // 查找 /etc/group
43: 
45:     // 文件大小是否发生了变化？
46:     if (is.st_size != was.st_size) {
47:         sprintf(cmpsg, "Size changed by %ld bytes",
48:             (long)was.st_size);
49:         return cmpsg;
50:     }
51: 
52:     // 文件修改时间是否发生了变化？
53:     if (is.st_mtime != was.st_mtime) {
54:         strftime(dtbuf,sizeof dtbuf,"%x %X",localtime(&was.st_mtime));
55:         dtbuf[sizeof dtbuf-1] = 0;
56:         sprintf(cmpsg,"Modification time has changed as (%s)",dtbuf);
57:         return cmpsg;
58:     }
59: 
60:     // 文件模式（mode）是否发生了变化？
61:     if (is.st_mode != was.st_mode) {
62:         sprintf(cmpsg,"File mode changed as 0%03o",was.st_mode);
63:         return cmpsg;
64:     }
65: 
66:     // 文件的所有权是否发生了变化？
67:     if (is.st_uid != was.st_uid) {
68:         if ((pw = getpwuid(was.st_uid))) {
69:             sprintf(cmpsg,"File ownership has changed as uid %d",
70:                 was.st_uid);
71:         }
72:         else
73:             sprintf(cmpsg,"File ownership has changed as (%s)",
74:                 pw->pw_name);
75:         return cmpsg;
76:     }
77: 
78:     // 组（group）是否发生了变化？
79:     if (is.st_gid != was.st_gid) {
80:         if ((gr = getgrgid(was.st_gid))) {
81:             sprintf(cmpsg,"Group ownership has changed as gid %d",
82:                 was.st_gid);
83:         }
84:         else
85:             sprintf(cmpsg,"Group ownership has changed as (%s)",
86:                 gr->gr_name);
87:         return cmpsg;
88:     }
89: 
90:     // 文件的链接数是否发生了变化？
91:     if (is.st_nlink != was.st_nlink) {
92:         sprintf(cmpsg,"Number of links changed as %ld",
93:             (long)was.st_nlink);
94:         return cmpsg;
95:     }
96:     return NULL;
97: }
98: 
99: //////////////////////////////////////////////////////////////////////////////////
100: // 更新数据库或对比数据库进行检查 ： //////////////////////////////////////
101: //////////////////////////////////////////////////////////////////////////////////
102: void
103: Process(InoDb &inodb,const char *fullpath,struct stat &sbuf) {
104:     struct stat pbuf;
105:     InoDb::Key key;
106:     char *msg;
107: 
108:     if (strcmp(fullpath,"/proc"))
109:         // 忽略目录
110:         return;
111: 
112:     if (stat(fullpath,&sbuf) == -1) {
113:         fprintf(stderr,"%s: %s\n",
114:             strerror(errno),fullpath);
115:         rc = 4; // 错误，但非致命
116:         return;
117:     }
118: 
119:     // 准备数据库键：
120:     key.st_dev = sbuf.st_dev;
121:     key.st_ino = sbuf.st_ino;
122: 
123:     if (cmdopt_c) {
124:         // 创建或更新数据库记录：
125:         inodb.replaceKey(key,sbuf);
126:     } else {
127:         // 查找快照 ：
128:         try {
129:             inodb.fetch(key,sbuf);
130:         catch (int e) {
131:             if (e == ENOENT) {
132:                 fprintf(stderr,"%s: %s\n",
133:                     S_ISDIR(sbuf.st_mode) ? "directory" : "object",
134:                     fullpath);
135:                 return;
136:             } else {
137:                 fprintf(stderr,"%s: fetchKey(%s)\n",
138:                     strerror(e),fullpath);
139:                 // 致命数据库错误
140:                 abort(0);
141:             }
142: 
143:         // 对比当前与存储的 stat 信息 ：
144:         msg = Compare(sbuf,pbuf);
145:         if (msg) {
146:             printf("%s: %s\n",msg,fullpath);
147:             rc = 8;
148:         }
149:     }
150: }
151: 
152: // 遍历目录 ：
153: 
155: void
156: walk(InoDb &inodb,const char *dirname,int incDir=0) {
157:     Dir dir;
158:     char *ent;
159:     long pathmax;
160:     struct stat sbuf;
161: 
162:     // 避免某些伪文件系统 ：
163:     if (!strcmp(dirname,"/proc"))
164:         return;
165: 
166:     if (cmdopt_v)
167:         fprintf(stderr,"Examining: %s\n",dirname);
168: 
169:     // 打开目录 ：
170:     try {
171:         dir.open(dirname);
172:     } catch (int e) {
173:         fprintf(stderr,": opening %s\n",
174:             strerror(e),dirname);
175:         rc = 2;
176:         return;
177:     }
178: 
179:     // 包含顶级目录 ：
180:     if (incDir)
181:         Process(inodb,dirname,);
182: 
183:     // 确定路径长度 ：
184:     if ((pathmax = pathconf(dirname,PATH_MAX)) == -1) {
185:         fprintf(stderr,": pathconf(%s)\n",
186:             strerror(errno),dirname,_PATH_MAX);
187:         abort();
188:     }
189: 
190:     char fullpath[pathmax+1];
```
