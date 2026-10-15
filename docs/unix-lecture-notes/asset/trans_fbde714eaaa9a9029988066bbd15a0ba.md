
FTS_DOT 未指定为 fts_open() 的文件名的名为 "." 或 ".." 的文件（请参阅 FTS_SEEDOT）。

FTS_DP 以后序方式访问的目录。FTSENT 结构的内容将保持不变，自其以先序方式返回时起，即 fts_info 字段设置为 FTS_D。

FTS_ERR 这是一个错误返回，fts_errno 字段将被设置为指示导致错误的原因。

FTS_F 一个普通文件。

FTS_NS 一个没有可用 stat 信息的文件。fts_statp 字段的内容未定义。这是一个错误返回，fts_errno 字段将被设置为指示导致错误的原因。

FTS_NSOK 一个未请求 stat 信息的文件。fts_statp 字段的内容未定义。

FTS_SL 一个符号链接。

FTS_SLNONE 一个目标不存在的符号链接。fts_statp 字段的内容引用符号链接本身的文件特征信息。

从上述信息中可以立即得出的一些观察是：

- fts_info 成员具有与 nftw() 函数通过 (*fn) 函数传递的整数中发现的信息类似的信息。
- 与 nftw() 函数不同，fts 为应用程序提供了钩子。特别是，fts_number 和 fts_pointer 是返回结构中的两个成员，可用于应用程序特定数据，从而可以在 fts_read() 函数的不同调用之间更改状态和数据。
- fts_parent 字段提供了一种访问父节点的方法，而 nftw() 则没有。
- 除非 fts_info 为 FTS_NS 或 FTS_NSOK，否则返回的文件的 stat 信息位于 fts_statp 成员中。
- 文件名位于 fts_name 成员中。fts_path 成员具有相对于搜索根的文件路径。实际上，这与 fts_accpath 相同。

还重要的是要知道，单个缓冲区用于文件层次结构中所有 FTSENT 结构的所有各种路径成员。因此，不能保证先前返回的 FTSENT 结构的 fts_path 和 fts_accpath 成员仍然正确以空字符结尾，因为它们可能已经被覆盖。只有 fts_read() 最近返回的文件的 fts_path 和 fts_accpath 成员保证以空字符结尾。要使用这些字段引用其他 FTSENT 结构表示的任何文件，需要使用该 FTSENT 结构的 fts_pathlen 字段中包含的信息修改路径缓冲区。在尝试进一步调用 fts_read() 之前，应撤销此类修改。相比之下，fts_name 字段始终以空字符结尾。

```
/********************************************************************************/
void usage(char* progname)
{
    printf("usage: %s directory pattern\n", progname);
}
/********************************************************************************/

void pmatch(char *dir, const char *pattern)
{
    FTS *tree;    /* pointer to file tree stream returned by fts_open */
    FTSENT *f;    /* pointer to structure returned by fts_read */
    char *argv[] = { dir, NULL };

    /* Call fts_open() with FTS_LOGICAL to follow symbolic links
     * including links to other directories. Since it detects cycles,
     * we do not have to worry about infinite loops.
     */
    tree = fts_open(argv, FTS_LOGICAL, entcmp);
    if (tree == NULL)
        perror("fts_open");

    /* Repeatedly get next file, skipping "." and ".." because
     * FTS_SEEDOT was not set.
     */
    while ((f = fts_read(tree))) {
        switch (f->fts_info) {
        case FTS_DNR:  /* Cannot read directory */
            fprintf(stderr, "Could not read %s\n", f->fts_path);
            continue;
        case FTS_ERR:  /* Miscellaneous error */
            fprintf(stderr, "Error on %s\n", f->fts_path);
            continue;
        case FTS_NS:   /* stat() error */
            /* Show error, then continue to next files. */
            fprintf(stderr, "Could not stat %s\n", f->fts_path);
            continue;
        case FTS_DP:
            /* Returned to directory for second time as part of
             * post-order visit to directory, so skip it. */
            continue;
        }

        /*
         * Check if the name matches pattern, and if so, print out its
         * path. This check uses FNM_PERIOD, so "*.c" will not
         * match ".invisible.c".
         */
        if (fnmatch(pattern, f->fts_name, FNM_PERIOD) == 0)
            printf("%s\n", f->fts_path);
