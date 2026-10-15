
![](img/0b91ab198b0fdfd564d5d19571459e_532_0.png)

Ruby 的这一方面类似于 Ada 的泛型能力。Ada 泛型允许参数化，不仅针对值，也针对类型。

## 异常处理

异常是语言处理动态或用户定义错误的方式。简单来说，语言支持设置异常处理器来捕获运行时错误。例如，你可能想要构建一个方法计算数字的平方。这很容易实现，如列表 26.18 所示。

### 列表 26.18 简单的平方方法

```ruby
def square(x)
  return x*x
end
```

然而，当你传递无效内容时会发生什么？这里有一个示例（见列表 26.19）。

### 列表 26.19 错误的类型

```ruby
irb(main):4> square("hello")
TypeError: can't be coerced into Integer
from 'square' in 'in:'
```

所示，错误是因为 `*` 方法无法应用于 `String`。你可以在列表 26.20 中看到这一点。情况下，`raise` 方法会将错误返回给调用者。

### 列表 26.20 抛出异常

```ruby
def square(x)
  if x.class != Fixnum
    raise "Not a number"
  end
  return x*x
end
```

```ruby
=> nil
irb(main):6> square(5)
=> 25
irb(main):7> square("hello")
RuntimeError: Not a number
from 'square' in 'in:'
```

在这种情况下，真正需要的是是抛出异常，还要捕获它。这出乎意料地通过一个名为 `rescue` 的关键字来实现。你可以在列表 26.21 中看到这一点。在 `square` 方法中，你抛出了名为 `AttributeError` 的异常。你定义了一个以 `begin` 开始的块，其中包含 `rescue` 子句。如果块内发生异常，则调用 `rescue`。注意这里 `rescue` 子句是根据要捕获的特定异常命名的。它也可以不命名以捕获所有异常。

### 列表 26.22 执行异常测试方法

```ruby
def test
  begin
    puts square(5)
    puts square("hello")
  rescue ArgumentError
    puts "Recover from this error!!!"
  end
  puts "done"
end
```

```ruby
irb(main):27> test
25
Recover from this error!!!
done
=> nil
```

## 内省

内省（或反射）是指语言在运行时检查自身的能力。内省的一个方面是在运行时枚举生存对象的能力。Ruby 提供了一个名为 `ObjectSpace` 的有趣模块提供了这种能力。你可以通过仅遍历特定类或模块的对象来精化这种操作。这在列表 26.23 中得到了演示。

### 列表 26.23 枚举所有数值对象

```ruby
irb(main):040:0> ObjectSpace.each_object(Numeric) {|x| puts x}
2.718218284905
3.14159265358979
2.2204460925031e-16
1.79769313486232e+308
2.22507385072e-308
=> 5
irb(main):041:0>
```

`ObjectSpace` 模块也可以用于为其他对象添加终结器（finalizers）。终结器是在特定对象被销毁时调用的 `proc`。该操作在列表 26.24 中显示。代码创建了一个示例类（`Dog`），然后是该类的一个实例（`dog`）。包含了 `ObjectSpace` 模块，这样你就不需要在在方法前指定其前缀。通过调用 `define_finalizer` 创建终结器。这包含了你的对象以及一个在对象被垃圾回收之前调用的简单 `proc`。你强制移除对象，并调用 `garbage_collect`（`ObjectSpace` 模块的一部分）最终移除调用终结器的对象。

### 列表 26.24 为对象创建终结器

```ruby
irb(main):001:0> class Dog
irb(main):002:1> end
=> nil
irb(main):003:0> include ObjectSpace
=> Object
irb(main):004:0> dog = Dog.new
=> #<Dog:0xb7d371c4>
irb(main):005:0> define_finalizer(dog, proc {|id| puts "bye #{id}"})
=> [0, #<Proc:0xb7d1ca18@(irb):6>]
irb(main):006:0> dog = nil
=> nil
irb(main):007:0> garbage_collect
bye -605436738
=> nil
```
