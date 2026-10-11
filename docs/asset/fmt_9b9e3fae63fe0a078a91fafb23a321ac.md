
字符串 `'x + 1'` 在代码运行时被翻译并执行，结果是打印 4。请注意，即使在运行时评估期间，绑定到变量 `x` 的值也可用。以下 Ruby 代码展示了一种人为构造的方法，用于找出 1 到 100 之间所有整数之和的结果。我们不是使用普通的循环或迭代方法，而是生成一个包含表达式 `"1+2+3...+99+100"` 的大字符串，然后对其进行求值：

```ruby
puts eval((1..100).to_a.join('+'))
```

`eval` 函数应谨慎使用。如果用作 `eval` 参数的字符串来自不可信来源（例如，来自用户输入），它可能是潜在的危险的（想象一下，如果待评估的字符串包含 Ruby 表达式 `rm -rf *` 会发生什么）。在许多情况下，`eval` 的替代方案更灵活，安全性更高，并且不需要在运行时解析代码带来的速度损失。

## Quine（自生程序）

Quine 是一种特殊的源代码生成器。术语文件将 quine 定义为“一个程序，其完整输出是其自身源代码的副本”。如果你认为这本身缺乏任何实用价值，那可能是正确的，但作为脑力挑战，它可以令人叹为观止。以下是 Ryan Davis 编写的一个 quine，它是 Ruby 语言中最短的之一：

```ruby
f='"%s";puts f%%f"';puts f%f'
```

运行此程序，你将得到它作为输出。你甚至可以从 shell 提示符尝试类似以下操作：

```bash
ruby -e 'f="%s";puts f%%f"';puts f%f' | ruby
```

这里我们使用命令行上的 `-e` 选项来指定一行要执行的 Ruby 源代码，然后使用管道将其输出发送到另一个 Ruby 解释器实例。输出再次是相同的程序源代码。

## 在运行时修改程序

动态语言，如 Ruby，允许你在运行时轻松修改程序的不同部分，而无需像之前那样显式生成源代码。Ruby 的核心 API 和框架（如 Ruby on Rails）利用此功能来自动化常见的编程任务。例如，在类定义中，你可以使用 `attr_accessor` 方法为给定的属性名称自动生成读/写访问方法。因此，以下代码：

```ruby
class Person
  attr_accessor :name
end
```

等效于以下更冗长的代码：

```ruby
class Person
  def name
    @name
  end

  def name=(new_name)
    @name = new_name
  end
end
```

前面的代码有一个小缺点：对应的实例变量 `@name` 实际上直到你首次设置其值时才创建。这意味着如果你恰好在写入之前读取此属性，你将得到 `nil` 值。如果不仔细，这可能会在你的程序中引入一些细微的 bug。避免此问题的最简单方法是在 `Person#initialize` 方法中将 `@name` 实例变量设置为一个合理的值。由于这是一个相当常见的场景，除了读/写访问器之外，自动拥有这个方法不是更好吗？让我们定义一个 `attr_initialize` 方法，使用 Ruby 的元编程功能来实现这一点。首先，让我们简要介绍两个对我们期望的元编程魔法至关重要的方法：

`cls.define_method(name) { body }`

这为接收类添加一个新的实例方法。它接受方法的名称（作为符号或字符串）和其主体（作为代码块）作为输入：

`obj.instance_variable_set(name, value)`

上述代码将实例变量绑定到指定值。实例变量的名称应该是符号或字符串，并且还应包括 `@` 前缀。

现在，我们准备好将 `attr_initialize` 类方法定义为 `Object` 类的扩展，以便任何其他类都可以使用它：

```ruby
require 'generator'

class Object
  def Object.attr_initialize(*attrs)
    define_method(:initialize) do |*args|
      if attrs.length != args.length
        raise ArgumentError,
          "wrong number of arguments (" +
          "#{args.length} for #{attrs.length})"
      end

      SyncEnumerator.new(attrs, args).each do |attr, arg|
        instance_variable_set("@#{attr}", arg)
      end
    end

    attr_accessor *attrs
  end
end
```

`attr_initialize` 方法接受可变数量的属性名称（`attrs`）作为输入。每个属性名称在动态创建的 `initialize` 方法参数列表（`args`）中都有相同的位置，以便设置其初始值。我们启动新方法的代码，检查收到的参数数量是否与最初指定的属性数量相同。如果不同，我们抛出带有描述性消息的错误。之后，我们使用 `SyncEnumerator` 对象（来自 `generator` 库）同时迭代已声明的属性列表（`attrs`）和实际参数列表（`args`），以使用 `instance_variable_set` 方法逐个执行属性-参数绑定。最后，我们委托给 `attr_accessor` 方法，以便为所有声明的属性创建读写访问方法。

以下是使用 `attr_initialize` 方法的方式：

```ruby
class Student
  attr_initialize :name, :id, :address
end

s = Student.new('Erika', 123, '13 Fake St')
s.address = '13 Wrong Rd'
puts s.name, s.id, s.address
```

预期的输出将是：

```text
Erika
123
13 Wrong Rd
