
默认情况下，每次都会检查碰撞。目前使用`Static`方法来收集它们。`BoundingSphere`存在于“世界”坐标系中。因此，当位置或旋转变化时，需要更新它——在高级引擎中，可以通过将`BoundingSphere`存储在单独变量中来节省计算。

这样，我们就可以检查碰撞了。目前，通过以下代码判断猿类是否与球体紧密接触即可：

```cpp
protected void update(Game gameTime) {
  foreach(ModelClass c in balls) {
    c.UpdatePos();
    if (myApe.myPosition.Intersects(c.BoundingSphere)) {
    }
  }
}
```

```cpp
protected void LoadContent() {
  for (int i = 0; i < 10; i++) {
    balls[i].myPosition = new Vector3(4, 0, 0);
    balls[i].myScale = -0.1f;
    balls[i].myRotation = 0;
    balls[i].myID = 0;
  }
  // 使用此内容加载你的游戏内容
  myCube = new Cube();
}
```

测试物理时，设置密度是一个类工作。对于我们的情况，对`LoadContent`进行以下修改即可：

在上面的`Converter 2013`中，我们发现以二进制创建的文件适用于

# 结论

尽管我们的立方体是为了真实游戏设计的，但目前的进展仍然需要尝试各种有趣的技术，这些技术可以各种方式应用于专业和独立游戏标题。

# 教程：链表

## 计算机科学：处理链表

![](img/a54b3b473771472dd2321ddda1014be1_47_0.png)

`Mihalis Tsoukalos` 是一位 `Unix` 管理员、`Unix` 和 `iOS` 程序员、`DBA` 以及许多其他身份。自 1993 年以来一直使用 `Linux`。

### 资源
- 文本编辑器
- `GCC` 编译器

# 通过创建、操作和排序链表来构建你的数据，以简化遍历和编辑

严格来说，链表是一个具有有限元素集的结构。每个元素至少包含两个位置：一个用于数据，另一个用于指针，将当前元素连接到构成列表元素序列中的下一个元素。这也被称为单向链表。

链表允许你随心所欲地删除或插入元素。此外，可以在任何类型的列表上执行的操作都易于理解且代码简单；你不需要编写很多代码，或在代码中设置限制。

一种链表，其中每个元素都从一端（头）插入并从另一端（尾）移除。

定义链表时，你应该做的第一件事是将链表的头部保存在变量中。头部是访问列表所唯一需要的内容。

链表最大的优势是它们易于理解、易于实现，并且足够通用，可以用于许多不同的情况和各种类型的程序中。

链表的查找函数是最重要的函数，因为它决定了元素是否在链表中，取决于你想对它做什么。查找函数越快返回答案，对你就越好，你会越快知道自己在链表中的位置，程序运行得也越快。

![](img/a54b3b473771472dd2321ddda1014be1_47_1.png)

可用的教程文件：`filesilo.co.uk`

# 理论

链表的第一个元素称为头（`head`），而最后一个元素通常称为尾（`tail`）。队列是一个

## 编写链表

`C` 程序生成了一个未排序的链表。在内部，链表的每个节点都如下所示：

### 简单的链表

#### 头 (`Head`)

#### 尾 (`Tail`)

![](img/a54b3b473771472dd2321ddda1014be1_48_0.png)

最后一个节点的下一个指针指向`NULL`，以表示我们已经到达末尾。定义的结构只有一个用于存储数据的变量，但你可以自由在节点内声明许多变量。

```c
typedef struct node {
    char *data;
    struct node *next;
};
```

成功调用`malloc`会返回一个指向分配内存的指针。如果发生错误，`malloc()` 返回`NULL`。这两行代码用于检查`malloc`的返回值：

```c
new_node = malloc(sizeof(*node));
if (new_node == NULL) {
    return 0;
}
```

一旦创建了新节点，你还需要为数据分配内存，因为它是一个字符串指针，通过以下方式完成：

```c
new_node->next = next;
*list = new_node;
```

每个新节点都插入在未排序链表的前部，并成为链表的头：

是时候稍微介绍一下`create.c`的链表实现了，它是本教程的基础。

## 创建排序列表

链表不仅可以帮助你轻松地排序数据，还可以帮助你在插入或删除后保持数据处于排序状态。从未排序列表中删除元素与上述相同；然而，插入到排序列表中是

# 优势与缺点

链表适用于顺序查找，特别是当有大量插入和删除时。如果列表有大量元素，元素的搜索时间可能会非常慢。

此外，未排序列表在搜索元素时可能非常慢。拥有 150,000 个节点的未排序链表将非常慢！链表也有一个优势：可以在它们上添加或删除元素。

两个函数`insert()` 和`lookup()` 分别用于添加新节点和查找元素。这两个函数都接受参数：链表头和值，以确定其是否存在，并在成功时返回`1`，失败时返回`0`。

正如你可以看到的，排序列表有许多优势。然而，插入到排序列表中的代价是昂贵的，因此要尽可能保持列表排序。然而，插入到排序列表并不容易。

如果你需要管理大量的排序元素并快速搜索它们，那么你最好使用树结构而不是链表；你将付出的代价是你将会失去链表的简单性；然而，你需要更多的内存来创建和保持树或哈希表的有序性或平衡。

...不相同，因为新节点必须进入正确的位置以保持列表排序。下所示的`createsorted.c`中的`C`代码创建了一个排序列表，并且它的基础是`createdosort.c`。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

typedef struct node {
    int data;
    struct node *next;
};

void LinkedList(node *list) {
    node *e;
    e = list;
    int n = 0;
    while (e != NULL) {
        printf("%i", e->data);
        n++;
        e = e->next;
    }
    printf("\nThe Linked List has %d nodes.\n", n);
}
```

```c
int insert(node **list, int value) {
    if (lookup(list, value)) {
        return 0;
    }
    node *node;
    node *temp;
    node *previous;
    node *start = *list;
    // create new node
    new_node = (node *)malloc(sizeof(node));
    //check whether node is created or
    if(new_node == NULL)
```

```c
printf("Insufficient memory.");
return 0;
}
```

```c
//Updating different parts of the node
new_node->data = value;
new_node->next = NULL;
```

```c
//checking whether the node is only or not
if (start == NULL) {
    start = new_node;
}
```

```c
//If value is less than the first node
else if (start < data) {
    new_node->next = list;
    start = new_node;
}
```

```c
else {
    previous = start;
    temp = start->next;
}
```

```c
//Go to position is to be inserted
while(temp != NULL && value > temp->data) {
    previous = temp;
    temp = temp->next;
}
```
