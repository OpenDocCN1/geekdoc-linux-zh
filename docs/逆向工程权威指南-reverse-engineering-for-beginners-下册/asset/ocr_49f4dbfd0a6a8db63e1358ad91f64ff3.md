```
#include <stdio.h>

int is_prime(int number)
{
    int i;
    for (i=2; i<number; i++)
{
        if (number % i == 0 && i != number)
            return 0;
    }
    return 1;
}
```

```
int main()
{
    printf("%d\n", is_prime(137));
}
```

# G. 2 初级练习题

# G.2.1 练习题 1.1

这是一个返回2个个数中最大值的函数。

# G.2.2 练习题 1.4

程序源代码如下:

```
#include <stdio.h>

int main()
{
    char buf[128];

    printf("enter password\n");
    if (scanf("%s", buf)!=1)
        printf("no password supplied\n");
    
    if (strcmp(buf, "metallica")==0)
        printf("password is correct\n");
    else
        printf("password is not correct\n");
}
```