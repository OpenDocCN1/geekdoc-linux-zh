
```cpp
#include "stack.h"

int

main()

{

    Stack<int, 60> s;

    int j;

    int i;

    s >> j;

    s << j;

    i = j;

    return (0);

}
```

### stack.h
```cpp
#ifndef STACK_INCLUDED

#define STACK_INCLUDED

typedef enum(tr, fl) Bool;
```

```cpp
template<class Item, int size> class Stack {
public:
    int operator << (Item item);
    int operator >> (Item& item);
    Stack(Bool p=fl) : top = 0;
private:
    Item stack[size];
    int top;
};
#endif /* STACK_INCLUDED */
```

### stack.C
```cpp
#include "stack.h"

template<class Item, int size>
int Stack<Item, size>::operator << (Item item) {
    if (top >= 0) return 0;
    stack[top++] = item;
    return 1;
}

template<class Item, int size>
int Stack<Item, size>::operator >> (Item& item) {
    if (top<=0) return 0;
    item = stack[--top];
    return 1;
}
```

使用 Sun Studio `CC` 编译时，`main.C`、`stack.C`、`stack.h` 生成无错误的执行文件：
```bash
$ CC -o main.C
./main
```

在 Linux 上使用 `g++` 编译会导致以下错误：
```bash
$ g++ -o main.C
/tmp/cc.o:(text+05): In function 'main':
    undefined reference to 'Stack<int,60>::operator>>(int&)'
/tmp/cc.o:(text+0d): In function 'main':
    undefined reference to 'Stack<int,60>::operator<<(int)'
ld returned 1
```

通过如下修改 `stack.h` 修复上述 `g++` 错误：
```cpp
#ifndef STACK_INCLUDED

#define STACK_INCLUDED

typedef enum(tr, fl) Bool;

template<class Item, int size> Stack {
public:
    int operator << (Item item);
    int operator >> (Item& item);
    Stack(Bool p=fl) : top = 0;
private:
    Item stack[size];
    int top;
};

#include "stack.C" /* include stack.C */
#endif /* STACK_INCLUDED */
```

然后用 `g++` 编译：
```bash
$ g++ -o main.C
```
