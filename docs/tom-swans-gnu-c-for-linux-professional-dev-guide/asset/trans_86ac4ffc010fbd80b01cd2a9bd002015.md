
一是操作系统的链接器本身能处理模板实例化。所谓的 Borland 模型则需要一种专门编制的链接器。CFront 模型的缺点在于编译器复杂度大幅增加。当最终程序的许多组成部分缺失、需要在链接阶段创建时，编译器要生成构建最终程序所需的全部信息并不容易。

## GNU C++ 模型

根据你使用的 GNU C++ 版本不同，模板实例化可能采取多种形式，但其中任何一种都不会与上述描述完全吻合。你的第一种选择是直接容忍多个模板实例的存在，尤其是当你使用的是 GNU C++ 2.7.2 或更早版本时。每个使用模板的模块都会获得自己的一份类或模板实例。这虽然可行，但代价是效率降低、编译速度变慢，而且明显浪费内存和磁盘空间。

第二种选择是获取一个打过补丁的链接器，即所谓的 collect2 程序（通过目录链接重命名为 ld），它了解对象仓库（object repositories）。你的系统可能已经在使用 collect2，因为这个链接器能够在程序启动时（在 main() 调用之前）调用全局类构造函数，并在 main() 返回之后调用全局析构函数。普通的 UNIX 链接器做不到这一点，因此在这些系统上，collect2 被插入到链接过程中来处理这些特殊任务。打过补丁的 collect2 版本同样了解对象仓库，可用于链接模板实例化。

如果你拥有这个打过补丁的链接器，就可以用 g++ 的 `-frepo` 选项编译某个模块，生成一个以 `.rpo` 结尾的仓库文件。随后，链接器会利用这个文件来生成它所需要的模板实例化。尽管标准 GNU C++ 编译器能够生成 `.rpo` 文件，但除非你拥有打过补丁的链接器，否则这些文件毫无用处。

> 注意
> 对象仓库在 GNU C++ 2.7.2 及更早版本中属于实验性功能。如果你使用的是较旧的编译器，请查看以下网站获取 GNU C++ 的更新：
> http://egcs.cygnus.com

坦率地说，这两种解决方案都不那么吸引人。下面介绍另一种适用于所有 GNU C++ 实现的方法，尽管它需要额外的编程工作，但却是所有方案中最简单的一种。

## 处理链接器问题

如果你尝试使用模板，可能会遇到关于未解析函数的链接器错误。发生这种情况是因为链接器无法找到编译器为特定模块创建的模板实例化。下面的代码清单说明了这个问题。

### 清单 17.5 TEMPLATE.H

```
// A template class
//
template <class T>
class TAnyClass {
private:
    T data;
public:
    TAnyClass(const T arg) : data(arg) { }
    const T & GetData() const;
};

// A template function prototype
//
template <class T>
TAnyClass<T> * MakeObject(const T param);
```

template.h 头文件将 TAnyClass 声明为一个模板，它有一个类型为 T 的私有数据成员、一个用于初始化该数据的构造函数，以及一个返回 data 值常量引用的函数。与所有模板一样，类型 T 只是一个占位符——真正的类型将在稍后的模板实例化过程中确定。

头文件还声明了一个模板函数 MakeObject()。该函数接收一个类型为 T 的常量参数，并返回一个指向 TAnyClass<T> 新对象的指针。到目前为止一切正常。清单 17.6 即 template.cpp，实现了该模板模块。

### 清单 17.6 TEMPLATE.CPP

```
#include "template.h"
#include <string>

// A template class member function
//
template <class T>
const T & TAnyClass<T>::GetData() const
{
    return data;
}

// A template function
//
template <class T>
TAnyClass<T> * MakeObject(const T param)
{
    return new TAnyClass<T>(param);
}

// ====== Cut Here ======
// Explicit template instantiations for TAnyClass
//
template class TAnyClass<int>;
template class TAnyClass<double>;
template class TAnyClass<string>;
```
