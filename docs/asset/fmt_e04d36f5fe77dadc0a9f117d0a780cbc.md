
还有许多其他未在本节中提及的字符串函数。

## 结构体

数组允许将相同数据类型的信息组合在一起，并使用下标引用其内容。

C 还提供了一种称为结构体的工具，用于将信息组合在一起。结构体提供了一种将不同数据类型的信息组合在一起的方法，以便将它们作为单个实体进行处理。

使用结构体的原因有哪些？原因有几个。结构体允许程序员将逻辑相关的数据项组织在一个常见的内存结构下的通用名称下。例如，将与员工相关的个人信息组合在一起是合理的。员工有姓名、地址、薪资、福利、职位等。每个数据项都与员工在逻辑上相关，但由不同的数据类型组成。

结构体还减少了传递给函数的参数数量。如果某个函数想要打印它拥有的所有关于员工的信息，每个数据项都需要一个参数；姓名、地址、薪资等。当所有这些信息都被组合到一个结构体下时，只有该结构体会被传递到函数中。

结构体是提高可读性的绝佳工具。如果一个程序将其所有员工信息组合到一个数据结构中，查找起来会很容易。

使用以下语法声明结构体：

```c
struct tag {
    member_list;
} name_list;
```

关键字 `struct` 告诉编译器这是一个结构体声明，其成员列表用花括号（`{ }`）包围。

`member_list`（成员列表）包含构成结构体的其他数据类型信息，也可以包含其他结构体。

`tag`（标签）是结构体模板的标识符或名称。结构体模板描述了结构体的布局或设计；标签用于标识该模板。

`name_list`（名称列表）是结构体变量的标识符或名称列表。换句话说，用于引用该类型结构体的变量名列在 `name_list` 中。结构体的变量名代表了根据模板设计分配给计算机内存。

结构体的声明分为两步。首先声明结构体的布局或模板；其次声明变量并分配内存。这些步骤可以通过两步完成，也可以在同一个语句中完成。示例展示了通过两步声明结构体：

```c
struct employee_jobs
{
    char job_title[30];
    float monthly_salary;
    int job_level;
};
```

这包含了我们希望与结构体关联的所有元素。此声明不包括变量名；这是通过使用标签 `employee_jobs` 以以下格式完成的：

```c
struct employee_jobs manager;
```

变量 `manager` 的类型是 `struct employee_jobs`。

可以声明其他类型的 `employee_jobs`：

```c
struct employee_jobs analyst;
struct employee_jobs ceo;
```

引用结构体中的元素略有不同。使用结构体变量名后跟一个点，然后是成员名，即可访问结构体的成员。要设置 CEO 的薪资，请使用以下语句：

```c
ceo.monthly_salary = 60000.00;
```

结构体也可以整体作为单一参数传递给函数。请考虑图 14-24 中的示例。

## 图 14-24 将结构体传递给函数

```c
struct time
{
    int hour;
    int minute;
};

int time_in_minutes( struct time t );

main()
{
    struct time time_now;
    int minutes;

    time_now.hour = 10;
    time_now.minute = 15;

    minutes = time_in_minutes( time_now );

    printf("%d hours and %d minutes comes to a total of %d minutes\n",
        time_now.hour, time_now.minute, minutes);

    return;
}

/* function to calculate the total number of minutes */
int time_in_minutes( struct time t )
{
    int total_minutes;

    total_minutes = t.hour * 60 + t.minute;  /* add minutes */
    return( total_minutes );
}
```

请注意，传递给函数 `time_in_minutes` 的 `time_now` 结构体在函数声明中被声明为变量 `t`，并在函数体内作为 `t` 使用。另外，请注意，信息只是从 `time` 结构体中读取；`time` 结构体的内容未被更改。如果函数 `time_in_minutes()` 试图更改 `time` 结构体的内容，那么在 `main()` 函数中看不到这种变化。这是因为结构体的副本被传递给了函数。如果在 `time_in_minutes()` 函数中对结构体进行了任何更改，这些更改只会作用于副本，并且在返回 `main()` 函数后副本被销毁。

若要传递实际的结构体以便在函数内更改其内容，必须使用指针。指针将在下一节中讨论。

结构体可以是一个详细的话题；本节提供了简要概述。有关结构体的更多示例和信息，请参阅本章末尾推荐的书籍。

## 指针

本节涵盖的最后一个主题是指针。指针是一个相当高级的主题，也是 C 语言中最强大的特性之一。指针可以用于代替索引来访问数组元素，或允许在函数内更改参数。指针还允许 C 处理动态分配的内存。这意味着变量的大小不包含在声明中。它是在函数主体中处理的。

指针是内存中的一个位置，包含指向其他内容或指向内存中另一个位置的地址。指针的内容类似于之前使用的整数数据，除了这些数据可用于访问其他数据。

指针在计算机内存中可以是常量或变量的形式。可以定义和初始化指针变量。指针变量中的值可以更改。指针常量中的值，就像我们见过的其他常量一样，不能更改。

可以使用以下语法定义指针变量：

`data_type *pointer_name;`

`data_type` 与之前看到的数据类型相同。数据类型指明指针将指向的信息类型。如果指针要指向一个浮点数，则指针应声明为 `float *salary_ptr;`。图 14-25 描绘了这个概念。

![](img/75f39fc91296b889c0653851accdfd46_1097_0.png)

声明为指针的变量包含其“指向”的变量的地址。指针 `salary_ptr` 必须声明为 `float` 类型，因为它指向类型为 `float` 的变量 `salary`。

## 指针运算符

有两个运算符经常与指针一起使用。`address`（地址）运算符（`&`）用于获取地址。`indirection`（间接访问）运算符（`*`）用于访问地址位置处的值。这些运算符执行相反的操作。如果将它们并排放在一起，它们会相互抵消。将地址赋值给指针时，使用地址运算符（`&`）。使用指针访问数据时，使用间接访问运算符（`*`）。

图 14-26 说明了指针的用法。

```c
main()
{
    int a_number = 10, num_from_ptr;
    int *num_ptr;

    num_ptr = &a_number;    // take the address from variable a_number and put it into the pointer variable num_ptr

    num_from_ptr = *num_ptr; // access the value at the address found in num_ptr and put the value in num_from_ptr

    print(“a_number = %d, num_from_ptr = %d\n”,
          a_number, num_from_ptr);
}
```

图 14-26 程序中的指针操作。

`printf()` 语句产生以下输出：

```text
a_number = 10, num_from_ptr = 10
```

如果我们打印 `num_ptr` 中的值，输出将是 `a_number` 变量的地址。图 14-27 是该程序的图形表示。

### 步骤 1

```c
num_ptr = &a_number;
```

![](img/75f39fc91296b889c0653851accdfd46_1099_0.png)

变量 `a_number` 的计算机地址被复制到指针变量 `num_ptr` 中。

![](img/75f39fc91296b889c0653851accdfd46_1099_1.png)

此时指针变量 `num_ptr` 指向变量 `a_number`。

### 步骤 2

```c
num_from_ptr = *num_ptr;
```

![](img/75f39fc91296b889c0653851accdfd46_1099_2.png)

沿着在变量 `num_ptr` 中发现的地址到达变量 `a_number`；`a_number` 的内容被复制到变量 `num_from_ptr` 中。
