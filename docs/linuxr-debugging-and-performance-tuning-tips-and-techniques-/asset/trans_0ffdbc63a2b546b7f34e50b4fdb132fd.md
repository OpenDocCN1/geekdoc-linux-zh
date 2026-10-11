

## 7.2 V7 ls 代码

```c
136      for (i=0; i < argc; i++) {    *Get info about each file*
137        if ((ep = gstat(*"*"+argv_1), )==NULL)
138            continue;
139            ep->in_namep = *argv;
140            ep->iflags |= ISARG;
141        }
142        qsort(firstp, lastp - firstp, sizeof *lastp, compar);
143        slastp = lastp;
144        for (epp=firstp; epp<slastp; epp++) {   *Main code, see text*
145            ep = *epp;
146            if (ep->ltype=='d' && dflg==0 || !fflg) {
147                if (large>1)
148                    printf("%\ns: \n", ep->in_namep);
149                    lastp = slastp;
150                readdir(ep->>in_namep);
151                if (!fflg==0)
152                    qsort(slastp,slastp - slastp,sizeof *lastp,compar);
153                if (!flig || stigl)
154                    printf("total %d\n", t_blocks);
155                for (epi=slastp; epi<lastp; epi++)
156                    pen try ("epi" )
157            } else
158                pen try (ep);
159        }
160        exit (0);                *End of main()*
161    }
```

第 136–141 行遍历各个参数，收集每个文件的相关信息。`gstat()` 的第二个参数是一个布尔值：如果该名称是命令行参数则为真，否则为假。第 140 行为每个命令行参数在 `iflags` 字段中添加 `ISARG` 标志。

`gstat()` 函数将每个新的 `struct lbuf` 添加到全局 `flist` 数组中（第 137 行）。它还更新全局指针 `lastp`，使其指向该数组中的当前最后一个元素。

第 142–143 行使用 `qsort()` 对数组进行排序，并将 `lastp` 的当前值保存到 `slastp` 中。第 144–159 行遍历数组中的每个元素，根据具体情况打印文件或目录的信息。

关于目录的代码值得进一步解释：

```c
if (ep->ltype=='d' && dflg==0 || !fflg) ...
```

第 146 行。如果文件类型是目录，并且未提供 `-c` 选项，或者提供了 `-f` 选项，则 `ls` 必须读取该目录的内容，而不是打印目录本身的信息。

if (argc>1) printf("\n%s:\n", ep->ln_namep)

第 147-148 行。如果在命令行上指定了多个文件，则打印目录名和一个冒号。

lastp = slastp; readdir(ep->ln_namep)

第 149-150 行。将 `lastp` 从 `slastp` 重置。`flist` 数组作为一个两级文件名栈起作用。命令行参数保存在 `firstp` 到 `slastp - 1` 之间。当 `readdir()` 读取一个目录时，它将该目录内容对应的 `struct lbuf` 结构体推入栈中，起始位置为 `slastp`，结束位置为 `lastp`。图 7.1 对此进行了说明。

![](img/766b5597246d532412fad21b1c59ccec_246_0.png)

### 图 7.1

作为两级栈的 `flist` 数组

if (ffl!=0) qsort(slastp,lastp - slastp,sizeof *lastp,compar)

第 151-152 行。如果未启用 `-f`，则对子目录条目进行排序。

if (lfl || sfl) printf("total %d\n", tblocks)

第 153-154 行。对于 `-1` 或 `-s` 选项，打印目录中文件所占用的总块数。这个总数保存在变量 `tblocks` 中，并且对每个目录都会重置。`printf()` 的 `%d` 格式字符串在现代系统中等价于 `%ld`；它的意思是“打印一个长整型”。（V7 也有 `%1d`，见第 192 行。）

for (ep1=slastp; ep1<lastp; ep1++) pentry(*ep1)

第 155-156 行。打印子目录中每个文件的信息。请注意，V7 的 `ls` 在目录树中只下降一层。它缺乏现代的 `-R` “递归”选项。

```c
163 pentry(ap)                    void pentry(struct tbuf *ap)
164 struct tbuf *ap;
165 {
166     struct { char dminor, dmaor; };  Unused historical artifact from V6 ls
167     register t;
168     register struct tbuf *p;
169     register char *cp;
170
171     p = ap;
172     if (p->inum == -1)               Inode number
173         return;
174     if (!flg)                 Inode number
175         printf("%5u ", p->innum);
176     if (sflg)                 Size in blocks
177         printf("*4d ", nblock(p->lszies));
```

`pentry()` 例程打印关于文件的信息。第 172–173 行检查 `inum` 字段是否为 -1，如果是则返回。当 `p->lnum == -1` 为真时，该 `struct tbuf` 无效。否则，该字段是文件的 inode 编号。

第 174–175 行如果启用了 `-i` 选项，则打印 inode 编号。第 176–177 行如果启用了 `-s` 选项，则打印总块数。（如下文所示，这个数字可能并不准确。）

```c
178     if (!flg) {                      Long listing:
179         putchar(p->>lype);           – File type
180         pmode(p->>lflags);           – Permissions
181         printf("%2d ", p->>lnl);     – Link count
182         t = p->>luid;
183     if(gflg)
184         t = p->>lgid;
185     if (getname(t, tbuf)==0)           – User or group
186         printf("%-6.6s", tbuf);
187     else
188         printf("%~6d", t);
189     if (p->>ltype==’b’ || p->>ltype==’c’)  – Device: major and minor numbers
190         printf("%3d,%3d", major((int)p->>lszie), minor((int)p->>lszie));
191     else
192         printf("%7ld", p->>lszie);    – Size in bytes
193         cp = ct ime(&p->>ltime);       – Modification time
194     if (p->>ltime < year)
195         printf(" %~-7.7% -4.%s ", cp+4, cp+20); else
196         printf(" %~12.12s ", cp+4);
197     }
198     if (p->>flags&ISARG)               – Filename
199         printf("%s\n", p->>ln.namep);
200     else
201         printf("%.14s\n", p->>ln.lname);
202     )
```

第 178–197 行处理 `-1` 选项。第 179–181 行打印文件的类型、权限和链接数。第 182–184 行根据 `-g` 选项，将 `u` 设置为用户 ID 或组 ID。第 185–188 行检索对应的名称，如果可用则打印。否则，程序打印数值。

第 189–192 行检查文件是否为块设备或字符设备。如果是，则打印通过 `major()` 和 `minor()` 宏提取的主要和次要设备编号。否则，打印文件大小。

第 193–196 行打印相关时间。如果时间早于六个月前，代码打印月份、日期和年份。否则，打印月份、日期和时间（关于 `ctime()` 结果格式，参见第 6.1.3.1 节“简单时间格式化：asctime() 和 ctime()”，第 170 页）。

最后，第 198–201 行打印文件名。对于命令行参数，我们知道它是一个以零结尾的字符串，因此可以使用 `%s`。对于从目录中读取的文件，它可能不以零结尾，因此必须使用显式的精度 `%.14s`。

```c
204 getname(uid, buf)	int getname(int uid, char buf[])
205 int uid;		
206 char buf[];		
207 {			
208 		int j, c, n, i;			
209 				
210 		if (uid==lastuid)		Simple caching, see text
211 			return(0);			
212 		if(pwdl == NULL)		Safety check
213 			return(-1);			
214 		rewind(pwdl);		Start at front of file
215 		lastuid = -1;			
216 		do {				
217 			i = 0;				Index in buf array
218 			j = 0;				Counts fields in line
219 			n = 0;				Converts numeric value
220 			while((c=fgetc(pwdl)) != '\n') {		Read lines
221 				if (c==EOF)				
222 					return(-1);				
223 				if (c==':') {			Count fields
224 					j++;				
225 					c = '0';				
226 				}				
227 			if (j==0)			First field is name
228 				buf[i++] = c;				
229 			if (j==2)			Third field is numeric ID
230 				n = n*10 + c - '0';			
231 			}				
232 		} while (n != uid);		Keep searching until ID found
```

```c
233         buf[i++] = ‘\0’;
234         lastuid = uid;
235     return(0);
236  }
```

`getname()` 函数将用户或组 ID 编号转换为对应的名称。它实现了一种简单的缓存方案；如果传入的 `uid` 与全局变量 `lastuid` 相同，则函数返回 `0` 表示成功；此时缓冲区中已经包含了名称（第 210–211 行）。`lastuid` 初始化为 −1（第 33 行），因此在第一次调用 `getname()` 时此测试会失败。

`pwd` 已经打开，指向 `/etc/passwd` 或 `/etc/group`（参见第 126–130 行）。这里的代码检查打开是否成功，如果失败则返回 −1（第 212–213 行）。

令人惊讶的是，`ls` 并没有使用 `getpwuid()` 或 `getgrgid()`。相反，它利用了 `/etc/passwd` 和 `/etc/group` 的前三个字段（名称、密码、数字 ID）格式相同，且都使用冒号作为分隔符这一事实。

第 216–232 行实现了在文件中线性搜索。`j` 统计到目前为止看到的冒号数量：名称处为 0，ID 号处为 2。因此，在扫描该行时，它同时填充了名称和 ID 号。

第 233–235 行终止名称缓冲区，将全局变量 `lastuid` 设置为找到的 ID 号，并返回 `0` 表示成功。

```c
238    long                            long nblock(long size)
239    nblock(size)
240    long size;
241    {                               
242        return((size+511)>>9);
243    }
```

`nblock()` 函数报告文件占用了多少个磁盘块。此计算基于 `stat()` 返回的文件大小。V7 的块大小为 512 字节——即物理磁盘扇区的大小。

第 242 行的计算看起来有点吓人。`>>9` 是右移九位。这相当于除以 512，从而得到块数。（在早期硬件上，右移比除法快得多。）目前为止还算顺利。然而，即使是只有一个字节的文件也会占用一整个磁盘块。但是，‘1 / 512’ 的结果是零（整数除法会截断小数部分），这是不正确的。这解释了为什么要加 ‘size+511’。通过加上 511，代码确保了在除以 512 时，和会产生正确的块数。

