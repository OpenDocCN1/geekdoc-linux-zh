
# Tom Swan 的 Linux 的 GNU C++ 专业开发指南

![](img/6eab91cc30158075ed10d0cabbac9029_0_0.png)

![](img/6eab91cc30158075ed10d0cabbac9029_2_0.png)

## TRADEMARKS

All terms mentioned in this book are known to be trademarks or service marks have been appropriately capitalized. Que Corporation cannot attest to the accuracy of this information. Use of a term in this book should not be regarded as affecting the validity of any trademark or service mark.

## WARNING AND DISCLAIMER

Every effort has been made to make this book as complete and as accurate as possible, but no warranty or fitness is implied. The information provided is on an “as is” basis. The author(s) and the publisher shall have neither liability nor responsibility to any person or entity with respect to any loss or damages arising from the information contained in this book or from the use of the CD or programs accompanying it.

**Associate Publisher**  
John Pierce

**Development Editor**  
Erik Dafforn

**Managing Editor**  
Thomas F. Hayes

**Copy Editor**  
Geniel Breeze

**Indexer**  
Bill Meyers

**Proofreader**  
Maribeth Echard

**Technical Editor**  
Rich Blum

**Team Coordinator**  
Julie Otto

**Media Developer**  
Michael Hunter

**Production**  
Dan Harris  
Brad Lenser

### 警告和错误 64
- 你已被警告 65
- 犯错是人之常情 65
- 警告和错误选项 67
- 将警告转为错误 68
- 编译并运行脚本 69

### 编译器选项 70
- 可移植性选项 70
- 中间编译 71
- 编译过程 72
- 分离编译 74
- 引号与否 75
- 头文件选项 75
- 控制包含路径 76
- 优化代码 77
- 优化级别 78
- 是否优化 79

### 调试入门 79
- 为调试而编译 80
- 选择你的武器 81
- 使用 `gdb` 控制台调试器 82
- 使用 `xxgdb` X Window 调试器 84
- 在 `Emacs` 中运行 `gdb` 86
- 有用的调试器选项 87

总结 88

## 6 创建数据对象 89

### 数据声明 90
- 类型转换 91
- 标识符：好、坏和丑 91
- GNU C++ 保留字 92

### 简单数据对象 93
- 整数变量 94
- 限制 95
- 作为宏的常量 96
- 作为对象的常量 97
- 预定义常量 98

### 全局和局部变量 99
### 多个变量声明 100
### 枚举类型 101
### 布尔变量 103
### 字面值 104
### 字面常量范围 105
### 双宽整数 105
### 收尾 107
### 浮点变量 108

### 字符字符串 110
- 字符 111
- C 风格字符串常量 111
- C 风格字符串变量 111
- 大小很重要 112
- 无中生有 113
- 比较字符串 114
- 连接字符串 115
- 搜索子字符串 115
- 字符转义代码 116
- 字符串转换 118
- 炒杂烩字符串 119

### 数组和结构体 120
- 一维数组 120
- 多维数组 121
- 初始化数组 121
- 预初始化数组 122
- 初始化字符串数组 122
- 结构体 123

### 调试数据对象 124
- 识别错误 124
- 加载代码 125
- 其他数据调试命令 128
- 自动显示变量 129
- 分配值 129
- 设置基数 130
- 查找变量的类型 130
- 使用 `assert()` 宏进行调试 130
- 调试变量汇总 131

总结 132

## 11 使用指针管理内存 223

相互递归函数 217  
函数与分离编译 218  
调试函数 219  
跨过函数 220  
进入函数 220  
调试内联函数 221  
总结 222

### 分配内存 224
### 使用 `new` 和 `delete` 进行内存管理 224
### 内存泄漏 227
### 使用 `malloc()` 和 `free()` 进行内存管理 228
### 处理内存错误 230
### 使用指针的指针 231
### 动态字符串 231
### 指针算术 234
### 获取内存块的大小 234
### 动态数组 235
### 多维动态数组 236
### 向 `main()` 传递参数 238
### `getopt()` 函数 239
### 其他内存相关事项 245

### 调试动态内存 247
### 调试指针 247
### 调试被寻址的数据 248
### 调试程序选项 249
### 调试 `main()` 参数 250

总结 251

### 为什么使用面向对象编程？ 256
### 引入类 256
### 使用类和对象编程 260
### 构造函数 261
### 成员函数 262
### 构造对象 263
### 默认构造函数 266
### 拷贝构造函数 266
### 内联构造函数 267
### 重载构造函数 269
### 调试类对象 271

总结 273

### 销毁类对象 276
### 引入析构函数 276
### 使用指针寻址对象 277
### 动态对象 278
### 在类中使用指针 280
### 类内存管理 280
### 拷贝构造函数 283
### 初始化数据成员对象 289
### 多种风味的对象 292
### 参数类对象 292
### 对象函数结果 294
### 类对象数组 296
### 类对象的动态数组 296
### 类对象指针数组 297
### 类对象指针的动态数组 298
### 作为数据成员的对象数组 299
### 对象与模块化编程 300
### `TDate` 头文件 300
### `TDate` 模块 301
### `TDate` 主程序 304
### 类与数据隐藏 306

总结 306

### 类作为构建块 308
### 单继承 308
### 多继承 309
### 创建派生类 309
### `TCoordinate` 类 311
### 派生类构造函数 314
### 派生类析构函数 317
### 复制派生类对象 321
### 引入受保护成员 324
### 更改访问说明符 324
### 限定选定成员 325
### 调试派生类 326
### 检查对象构造 327
### 检查对象数据成员 328
### 调用成员函数 329
### 查找对象的类型 330

总结 330

### Poly Want a Morphism？ 332
### 创建容器类 334
### 抽象类 334
### 虚析构函数 335
### 纯虚函数 335
### `TContainer` 类 336
### 调用虚函数 338
### 从抽象类派生 342
### 多继承 345
### 加载基类 346
### 使用多个基类构造函数 346
### 使用虚基类 347
### 修复模糊基类 350
### 调试带虚函数的类 352
### 调试分离模块中的类 352
### 调试虚函数调用 354

总结 355

### 几个好术语 358
### 引入异常 358
### 抛出异常对象 359
### 标准 `exception` 类 360
### 引入 `try` 块 361
### 多个 `catch` 语句 362
### 嵌套 `try` 块 362
### 使用 `try` 块 363
### 使用异常编程 364
### 未处理的异常 367
### 替换 `unexpected()` 和 `terminate()` 368
### 捕获所有异常 369
### 异常与局部对象 373
### 异常与构造函数 374
### 到处抛自己的类的类 375
### 异常与内存管理 376
