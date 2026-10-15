
# 数据库模块

## 初始化与分配

我们在继续初始化 DB 结构。调用者传递的路径指定了数据库文件名的前缀。我们添加后缀 `.idx` 来创建数据库索引文件。

如果调用者想要创建数据库文件，请使用 `<stdlib.h>` 中的变参数函数来查找可选参数。然后，我们使用 `open` 创建索引文件和数据文件。如果数据文件的文件名与索引文件具有相同的前缀，但以 `.dat` 为后缀。

如果调用者没有指定 `O_CREAT` 标志，那么我们正在打开现数据库文件。在这种情况下，我们简单地调用带有两个参数的 `open`。

如果在打开或创建任何数据库文件时遇到错误，调用 `_db_free` 来清理 DB 结构并返回 NULL。如果一个成功，`_db_free` 将负责关闭已打开的文件描述符，稍后我们将释放它。

当正在创建数据库时，我们会遇到锁定问题。考虑两个进程同时尝试创建数据库。假设第一个进程调用了 `fstat` 并被内核阻塞，直到它返回。第二个进程调用 `db_open`，发现索引长度为 0，然后初始化空闲列表和哈希链。第二个进程向数据库写入了一条记录。此时，该进程被阻塞，而第一个进程在调用 `fstat` 后继续运行。第一个进程发现索引的大小为 0（因为在第二个进程初始化索引之前已经调用了 `fstat`），因此第一个进程初始化了列表和哈希链，从而抹除了存储在数据库中的记录。防止这种情况的方法是使用锁。我们使用了来自第 14.3 节的 `read_lock`、`write_lock` 和 `un_lock` 宏。

如果索引文件的大小为 0，说明我们刚刚创建了它，因此我们需要初始化空闲列表和哈希链指针。然后，它使用格式 `"%s"` 将数据库指针从整数转换为 ASCII 字符串。我们将在 `db_writeidx` 和 `db_writeptr` 中再次使用这种格式。该格式告诉 `sprintf` 使用 `PTR_SZ` 并其作为下一个参数的最小宽度，在本例中该参数为 0（因为我们正在创建一个新数据库，所以我们将指针初始化为 0）。这样做的效果是形成一个至少有 `PTR_SZ` 个字符的字符串（用空格填充）。实际上，我们传递的是一个值而不是 0，但我们会首先验证该值是否大于 `PTR_MAX`，以保证写入数据库的写入恰好是 `PTR_SZ`（6）字符。

```c
hash() = 0;
for (i = 0; i < HASH_DEF + 1; i++) {
    strcat(hash, asciptrt);
    strcat(hash, "\n");
}

i = strlen(hash);

if (write(db_open->idxfd, hash, i) != i) {

    err_dump("db_open: index file not write error");

}

if (un_lock(db)->idxfd, 0, SEEK, 0) < 0) {

    err_dump("db_open: un_lock error");

}

db_rewind(db);

return(db);

/* 分配并初始化 DB 结构及其缓冲区。 */

static DB *

db_alloc(int namelen) {

    DB *db;

    /* 使用 calloc 将结构初始化为零。 */

    if ((db->name = malloc(namelen + sizeof(char))) == NULL)

        err_dump("db_alloc: calloc error for DB");

    db->idxfd = db->datfd = -1; /* 描述符 */

    /* 为名称分配空间。 */

    if ((db->name = malloc(namelen + 5)) == NULL)

        err_dump("db_alloc: malloc error for DB");
```

## 查找与锁定

`db_find_and_lock` 函数在我们想要对搜索记录的索引文件上写锁时，会返回一个非零值。如果我们使用读锁（为零），则会在搜索时读取索引文件。

我们在 `_db_find_and_lock` 中遍历哈希链。将 `key` 转换为哈希值，并用它来计算文件中哈希链的起始地址（`chainoff`）。我们在遍历哈希链时等待锁被授予。注意，我们只锁定了哈希链的第一个字节。这通过允许多个进程同时搜索不同的哈希链，从而增加了并发性。

我们调用 `_db_readptr` 来读取哈希链中的第一个指针。如果它返回零，则哈希链为空。

```c
231 * 查找指定的记录。由 db_delete, db_fetch,
232 * 和 db_store 调用。返回时锁定哈希链。
233 */
234 static int
235 _db_find_and_lock(DB *db, const char *key, int itlock)
236 {
237 offset_t offset, offset;
238 /*
239 * 计算此 key 的哈希值，然后计算
240 * 在哈希表中对应 ptr 的字节偏移量。
241 * 这是我们的搜索起点。我们首先计算
242 * 该 key 在哈希表中的偏移量。
243 */
244 db->chainoff = _db_hash(db, key * PTR_SZ) + db->hashoff;
245 db->ptroff = db->chainoff;
246 /*
247 * 我们锁定哈希链。调用者必须在完成后
248 * 解锁它。我们锁定并只解锁第一个字节。
249 */
250 if (itlock) {
251     if (write_lock(db->ixfd, db->chainoff, SEEK_SET, 1) < 0) {
252         err_dump("db_find_and_lock: itwrite_lock error");
253     }
254 } else {
255     if (read_lock(db->ixfd, db->chainoff, SEEK_SET, 1) < 0) {
256         err_dump("db_find_and_lock: itread_lock error");
257     }
258 }
259
260 /* 获取哈希链上第一条记录在索引文件中的偏移
261 * （可以为 0）。
262 */
263 offset = _db_readptr(db, db->ptroff);
```

在循环中，我们遍历哈希链上的每条索引记录并比较 `key`。我们调用 `db_readdir` 读取读取每条索引记录。它用当前记录的字段填充 `idbuf`。如果 `_db_readdir` 返回零，说明我们到达了链的最后一个条目。

如果 `offset` 为零，说明我们在没有找到匹配 `key` 的情况下到达了哈希链的末尾，因此我们返回 -1。否则，我们找到了匹配项（通过 `break` 语句退出循环），因此我们返回 0。在这种情况下，`proff` 字段包含上一个索引记录的地址，`detail` 包含数据记录的地址，而 `datlen` 包含数据记录的大小。我们沿着哈希链移动，因为上一个索引记录指向当前索引记录。我们在删除记录时会用到这一点，因为我们必须修改指针记录来删除当前记录。

`_db_hash` 计算给定 `key` 的哈希值。它将 ASCII 字符乘以其从 1 开始的索引，并除以哈希表条目的数量。除法的余数就是该 `key` 的哈希值。注意，哈希表条目的数量为 137，这是一个质数。根据 Knuth (1998) 的说法，质数哈希提供了良好的分布特性。

```c
268 }
269 /*
270   发生错误时 offset == 0（未找到记录）。
271  *
272 return(offset == 0 ? -1 : 0);
273 */
274 /*
275   计算 key 的哈希值。
276  */
277 static DBASH
278 _db_hash(DBH *db, const char *key)
279 {
280   DBASH val = 0;
281   char c;
282   int i;
283   for (i = 1; (c = *key++) != 0; i++)
284     val += c; /* ascii 字符乘以其从 1 开始的索引 */
285   return(val % db->hash);
286 }
```

## 读取指针

```c
288 /*
289   从索引文件的任意位置读取指针字段：
290   空闲列表指针、哈希表链指针或
291   索引记录指针。
292   static off_t
293   _db_readptr(DB *db, off_t offset)
294 {
295   char ascript[PTR_SIZE + 1];
296   if (seek(db->ixfd, offset, SEEK_SET) == -1)
297     err_dump("db_readptr: db->ixfd, seek error to ptr field");
298   if (read(db->ixfd, ascript, PTR_SIZE) != PTR_SIZE)
299     err_dump("db_readptr: read error of ptr field");
300   ascript[PTR_SIZE] = 0; /* 终止符 */
301   return(atol(ascript));
302 }
```

## 读取索引记录

`db_readidx` 用于读取指定偏移处的记录。如果成功，函数将返回列表中下一个记录的偏移量。在这种情况下，函数将填充 DB 结构：`off` 索引文件中记录的偏移，`ptrval` 列表中下一个条目的偏移，`idxlen` 每个索引记录的偏移，`buf` 包含实际的索引记录，包含数据记录的偏移，`len` 数据记录的长度。

```c
303 /*
304 * 从指定的指定的偏移处读取下一条索引记录。
305 * 我们将索引记录读取到 db->buf 中，
306 * 并将指针替换为空字节。如果一切正常，
307 * 设置 db->off 和 db->len 为数据文件中
308 * 记录的偏移量和长度。
309 */
310 static off_t
311 db_readidx(DB *db, off_t offset)
312 {
313 size_t
314 char *ptr1, *ptr2;
315 char ascript[PTR_SZ + 1, IDXLEN_SZ + 1];
316 struct iov[2];
```

```c
317 /*
318 * 定位索引文件并读取偏移量。db_readidx
319 * 使用 offset=0 从当前偏移读取记录。
320 * 我们仍然需要调用 seek 来记录当前偏移。
321 */
322 if ((db->off = lseek(db->ixfd, offset,
323 offset == 0 ? SEEK_CUR : SEEK_SET)) == -1)
324     err_dump("db_readidx: lseek error");
325 /*
326 * 读取索引记录开头的链指针和 ascii 长度。
327 * 这告诉了我们索引记录的
328 * 剩余大小。
329 */
330 iov[0].iov_base = ascript;
331 iov[0].iov_len = PTR_SZ;
332 iov[1].iov_base = ascript;
333 iov[1].iov_len = IDXLEN_SZ;
334 if ((i = readv(db->ixfd, iov, 2)) != 2) {
335     if (i == 0 && offset == 0) {
336         return -1; /* db_nextrec 的文件结束符 */
337     }
```
