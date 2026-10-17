
```c
page->mapping = mapping;

page->index = offset;

mapping->nrpages++;

...

return error;

}
}
```

同样提供了具有相同定义的备用函数 `add_to_page_cache_lru`。它首先调用 `add_to_page_cache` 将页添加到特定的地址空间。

### 16.4. 查找页

将所有页保持在基数树结构中，当内核需要判断一个页是否被缓存时是非常有利的，提供了 `find_get_page` 用于此目的：

```c
mm/filemap.c

struct page * find_get_page(struct address_space *mapping, poff_t offset)
{
    struct page *page = radix_tree_lookup(&mapping->page_tree, offset);
    page_cache_get(page);
    return page;
}
```

文件偏移量与页偏移量之间的转换是将索引除以 `PAGE_CACHE_SHIFT`：

```c
index = ppos >> PAGE_CACHE_SHIFT;
```

# 第 16 章：页缓存与缓冲区缓存

`ppos` 是文件的字节偏移量，而 `index` 包含对应的页缓存偏移量。

为了方便起见，提供了两个辅助函数：

```c
<pagemap.h>

struct page * find_or_create_page(struct address_space *mapping,
    pgoff_t index, gpf_t gpf_mask);
struct page * find_lock_page(struct address_space *mapping,
    pgoff_t index);
```

`find_or_create_page` 的正如其名所示——它在页缓存中查找一个页，如果不存在则分配一个空闲页。该页将通过 `add_to_page_cache_lru` 插入到缓存和 LRU 列表中。

`find_lock_page` 的工作方式类似于逐页查找页。

> 注意：如果该页已经被内核的其他部分锁定，该函数将进入睡眠，直到该页被解锁。

也可以一次搜索多个页。以下是辅助函数的原型：

```c
<pagemap.h>

unsigned find_get_pages(struct address_space *mapping, pgoff_t start,
    unsigned int nr_pages, struct page **pages);
unsigned find_get_pages_contig(struct address_space *mapping, pgoff_t start,
    unsigned int nr_pages, struct page **pages);
unsigned find_get_pages_tag(struct address_space *mapping, pgoff_t index,
    int tag, unsigned int nr_pages, struct page **pages);
```

- `find_get_pages` 从映射中从页缓存偏移量开始返回最多 `nr_pages` 个页。指向页的指针放置在页数组中。该函数不保证页范围连续的——对于不存在的页可能会存在空隙。返回值为找到的页数。
- `find_get_pages_tag` 类似于 `find_pages`，但只选择具有特定 `tag` 的页。此外，`index` 参数指向结果页数组中最后一个页之后的紧邻页的页缓存索引。

## 16.4.3 等待页

内核经常需要等待页，直到其状态变为某些期望的值。例如，同步实现需要确保页写操作已完成，且内存中的内容与底层块设备上的数据一致。正在写回的页具有 `PG_writeback` 位。

提供了函数 `<pagemap.h>` 来等待直到该位消失：

```c
<pagemap.h>

static inline void wait_on_page_writeback(struct page *page)
{
    if (PageWriteback(page))
        wait_on_page_bit(page, PG_writeback);
}
```

`wait_on_page_writeback` 安装了一个等待队列，进程可以在该队列上睡眠，直到页标志中移除 `PG_writeback` 位。

同样，可能出现需要某个页被解锁的情况。`wait_on_page_locked` 负责处理这种情况。

## 16.4 针对整页的操作

现代设备——尽管其名称如此——在单次操作中传输的不仅仅是块，而是大得多的数据，从而提升了系统性能。这体现在内核对算法和结构的强烈关注上，这些结构将页作为块与设备之间传输的元素单元。在处理完整集合时，按缓冲区（Buffer-by-buffer）对性能起到了巨大的支撑。在重新设计块层的过程中，页在 2.5 版本的开发期间被引入，以替代缓冲区来处理与块设备的传输。内核中添加了四个新函数以支持一个或多个页的读写。

```c
<pagemap.h>

int mpage_readpages(struct address_space *mapping, struct list_head *pages,
    unsigned nr_pages, block_t get_block);
int mpage_readpage(struct page *page, get_block_t get_block);
int mpage_writepages(struct address_space *mapping,
    struct writeback_control *wbo, block_t get_block_t get_block);
int mpage_writepage(struct page *page, get_block_t get_block,
    struct writeback_control *wbo);
```

参数的含义从前面的章节中显而易见，唯一的异常是 `writeback_control`。正如第 17 章讨论的，这是一个用于精细控制写回操作的选项。

由于这四个函数的实现具有共同点（它们的目标始终为块层构建一个合适的 `bio` 实例），因此讨论将限于检查一个示例——`mpage_readpages`。该函数期望将 `nr_pages` 个页实例作为链表参数传入。`mapping` 是关联的地址空间，`get_block` 像常一样被调用以查找匹配的地址。

该函数循环遍历所有的页实例：

```c
fs/mpage.c

int
mpage_readpages(struct address_space *mapping, struct list_head *pages,
    unsigned nr_pages, get_block_t get_block);
```

```c
struct bio *bio = NULL;
unsigned page_idx;
sector_t last_block_in_bio = 0;
struct buffer_head_map *map_bh;
struct pagevec *pveec;
clear_buffer_head(map_bh);
for (page_idx = 0; page_idx < nr_pages; page_idx++) {
    struct page *page = list_entry(pages, struct page, lru);
    if (!add_to_page_cache(page, mapping, GFP_KERNEL)) {
        bio = mpage_readpages(mapping, page, nr_pages - page_idx, &last_block_in_bio, get_block());
    } else {
        page_release(page);
    }
}
```

页通过 `add_to_page_cache_lru` 安装到缓存和 LRU 列表中。当 `mpage_readpages` 构建请求时，然而，如果遇到异常情况（例如包含缓冲区），它将退回到逐页处理。

```c
fs/mpage.c
if (bio)
    mpage_bio_submit(bio);
```
