
### 链表的工作原理

哈希表使用链表来存储数据。必须使用链表吗？不，但链表有很多优势。链表非常擅长顺序查找，特别是当与 `C` 语言指针配合使用时：它们是一种简单而优雅的数据结构，可以动态增长，除了少数几个指针外不需要任何额外空间，并且在插入操作方面表现良好。最后，只要你不是经常从哈希表中删除元素，它们就不需要太多的维护工作。

然而，链表也有缺点。如果链表包含许多元素，到达列表的最后一个元素可能会非常慢。此外，当处理包含大量元素的数据时，链表也会非常慢：无论如何，包含 100,000 个节点的链表都会很慢！

即将推出的教程将更深入地讨论链表。目前，请查看 `linkedlist.c` 以获取更多信息。你会发现 `linkedlist.c` 中的代码与 `hashTable.c` 中的代码类似。

```c
void printHashTable(node *table[], const unsigned int tablesize)
{
    node *e;
    int i;
    int length = tablesize;
    printf("Printing a hash table with %d buckets\n", length);
    for(i = 0; i<length; i++)
    {
        e = table[i];
        int n = 0;
        if (e == NULL)
            printf("%4d| bucket %d\n", i);
        else
        {
            while( e != NULL )
            {
                n++;
                e = e->next;
            }
            printf("%4d| has %d key\n", i, n);
        }
    }
}

int main(int argc, char **argv)
{
    char word[50];
    char c;
    int found = 0;
    int notFound = 0;
    node *table[TABLESIZE] = {0};
    FILE *INPUT;
    INPUT = fopen("INPUT", "r");
    populate_hash(table, INPUT);
    fclose(INPUT);
    printf("You can now use the Hash Table!\n");
    int line = 0;
    FILE *CHECK;
    CHECK = fopen("CHECK", "r");
    do {
        c = fscanf(CHECK, "%s", word);
        size_t ln = strlen(word) - 1;
        if (word[ln] == '\n')
            word[ln] = '\0';
        line++;
        if (lookup(table, word))
            found++;
        else
            notFound++;
    } while (c != EOF);
    printf("Found %d words in the hash table!\n", found);
    printf("Not found %d words in the hash table\n", notFound);
    fclose(CHECK);
    return 0;
}
```
