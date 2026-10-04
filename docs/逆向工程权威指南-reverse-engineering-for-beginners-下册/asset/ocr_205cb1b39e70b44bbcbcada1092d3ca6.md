```
{
  rand_state=rand_state*RNG_a;
  rand_state=rand_state+RNG_c;
  return rand_state & 0x7fff;
}
```

程序启动初初始化了几个成员变量（Class Fields）。这是如何进行的呢？这就得借助javap查看该类的构造函数：

```
static ();
flags: ACC_STATIC
stack=1, locals=0, args_size=0 // int 166425
  0: ldc #5 // Field rand_a:I
  2: putstatic #3 // Field rand_a:I
  5: ldc #6 // int 101904223
  7: putstatic #4 // Field rand_c:I
  10: return
```

上述指令展示了变量的初始化过程。变量RNG_a和RNG_c分别参数的第三和第四槽单元。putstatic函数将有关数值存放在相应的地址。

函数my_rand(int)将输入值保存在变量rand_state中：

```
public void my_rand(int);
flags: ACC_PUBLIC
Code:
stack=1, locals=2, args_size=2
  0: iload_1
  2: putstatic #2 // Field rand_state:I
  4: return
```

iload_1指令提取输入变量，然后将其压入栈中。但是为什么在此处用iload_1而不是读取第0个参数的iland_0指令呢？由于该函数调用的类的变量，由于要用第0个参数传递this。以此类推，函数的第二个参数槽用于传递成员变量，同时是隐性参数rand_state，此后的putstatic指令将把栈的值存之第二个参数槽、完成指定任务。

我们来看看my_rand()函数：

```
public int my_rand();
flags: ACC_PUBLIC
Code:
stack=2, locals=1, args_size=1
  0: getstatic #2 // Field rand_state:I
  3: getstatic #3 // Field rand_a:I
  6: imul
  7: putstatic #2 // Field rand_state:I
```