```
};
void dump()
{
    printf("this is box. color=%d, width=%d\nheight=%d, depth=%d\n", color, width, \height, depth);
};

class sphere : public object
{
private:
    int radius;
public:
    sphere(int color, int radius)
    {
        this->color=color;
        this->radius=radius;
    }
    void dump()
{
        printf("this is sphere. color=%d, radius=%d\n", color, radius);
    }
};

int main()
{
    box b(1, 10, 20, 30);
    sphere s(2, 40);

    b.print_color();
    s.print_color();

    b.dump();
    s.dump();

    return 0;
}
```

我们共同关注dump()函数（又称方法）以及object::print_color()的指令代码，重点分析32位环境下数据类型的内存存储布局。

下面所示的是不同的类的dump()方法，它们是在启用优化编译选项/0x/0b后，由MSVC 2008产生的代码。