
在这个示例中，调试信息每两秒最多打印一次。这防止了控制台上信息的泛滥，计算机保持可用。根据你的需求，你可能需要更大或更小的速率限制。

```c
static unsigned long limit = 0;
```

```c
if (limit < 5) {
    limit++;
    printk(KERN_ERR "blah blah blah\n");
}
```
