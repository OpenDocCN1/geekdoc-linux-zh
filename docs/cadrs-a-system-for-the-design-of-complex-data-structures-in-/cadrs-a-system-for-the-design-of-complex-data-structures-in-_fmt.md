
# CADRS：一种用于 LISP 中复杂数据结构设计的系统

![](img/1c87f534ef795b1172565160a42cdede_0_0.png)

Richard J. Duncan

## 摘要

本论文描述了一个旨在为 LISP 设计并实现数据抽象设施的项目。该项目的成果 CADRS（一种与结构无关的数据访问编译器）系统，支持对混合数据/过程结构的定义、创建和高效操纵，这些结构非常类似于 Simula [2] 和 Smalltalk 等语言中的类对象。

Richard J. Duncan

Richard J. Duncan

这是一篇提交给宾夕法尼亚大学工程与应用科学学院的论文，旨在满足计算机与信息科学研究生工程硕士学位的学位要求。

Timothy W. Finin, 导师

O. Peter Buneman, 研究生小组主席

- 1 -

## 致谢

我要感谢许多人对这项工作所提供的帮助。首先，最感谢我的导师 Timothy W. Finin 博士，他在 CADRS 设计理念形成方面提供了无价的帮助，并对这项工作付出了持久的热情；感谢研究生系的教师和学生们，在需要答案时总是敞开大门，特别是 Marty Borowski 花时间校对校稿；最后，感谢我的家人和朋友的支持。

1984年7月3日

## 9. 模式 ............................................................................ 72

- 9.1 宏替换 ................................................................... 72
- 9.2 类型化 ...................................................................................... 73
- 9.3 路径检查 ....................................................................... 73

## 10. 异常处理 ....................................................................... 74

## 11. CADRS 工具包 ........................................................ 80

- 11.4 CADRSUTIL ....................................... 81
- 12.1 结语 ............................................................................ 83

## 1 - 引言

### 1.1 引言

本文描述了一个为 LISP 设计并实现数据抽象设施的项目。该项目的结果——CADRS（无结构数据访问编译器）系统，支持对混合数据/过程结构的定义、创建和高效操作，这些结构与 Simula [2] 和 Smalltalk 等语言中的类对象非常相似。

### 1.2 论文概述

本文旨在实现两个目的。首先是记录 CADRS 背后的设计哲学。其次是为希望使用该软件包¹ 的人员提供 CADRS 功能的参考。

本章的其余部分描述了 CADRS 的设计。讨论从对不同数据抽象形式形式的简要检查开始。接下来，简要概述了 CADRS 的功能。随后是对 CADRS 与其他 LISP 结构定义包的对比分析。本章以 CADRS 与 FRL（一种基于网络的知识表示方案）的对比结束。

- CADRS 目前在 Franz Lisp Opus 38 下实现，但可以很容易修改在 MACLisp 下运行。

后续章节详细介绍了 CADRS。这些章节（第 2 到第 11 章）旨在作为 CADRS 的参考手册。软件包中的每个用户级函数都得到了描述和示例说明。

最后一章给出了一些性意见和对未来工作的考虑。

### 1.3 数据抽象方案概述

正如 Worth 在 [9] 中指出的，“……[计算机]要处理的大量信息在某种意义上代表了现实世界某部分的抽象。” 这种处理的第一步是在计算机上开发这种抽象的表示。正如 Worth 所指出的，这种表示的最低层次（以及所有其他表示所映射的层次）是硬件（或 LISP 的虚拟机）所提供的数据结构和控制结构。高层语言中发现的数据抽象设施提供了更复杂的原语，允许在更具概念的层构建表示。

#### 1.3.1 基础数据抽象

PASCAL 提供了支持合理数据抽象的基础。首先是根据已定义的类型定义数据类型；其次是通过记录（RECORD）定义异构数据结构，允许对信息进行分组；第三是定义动态（递归）结构。

PASCAL 的结构定义方案并非没有局限性。作为说明，考虑以下实现反转列表栈的 PASCAL 程序：

# 3 July 1984

```pascal
program reverse (input,output);
type
  stack = ^stk;
  stk = record
    val : integer;
    nxt : stack
  end;
var
  i : integer;
  s : stack;

procedure push (v : integer; var s : stack);
var
  tmp_s : stack;
begin
  tmp_s := s;
  new(s);
  s^.val := v;
  s^.nxt := tmp_s
end;

function pop (s : stack) : integer;
begin
  pop := s^.val;
  s := s^.nxt;
end;

function empty (s : stack) : boolean;
begin
  empty := s = nil
end;

begin
  s := nil;
  write('enter value ');
  while not eof do
  begin
    readln(i);
    push(i, s);
    write('enter value ')
  end;
  writeln('the reversed list is');
  while not empty(s) do writeln(pop(s))
end.
```

`push` 和 `pop` 过程将程序员与栈的底层结构隔离开。不幸的是，直接操作结构的便利性诱使程序员偶尔这样做，而不是编写必要的函数/过程（例如使用 `s := nil`，而不是初始化栈的函数/过程）。因此，对 `stack` 结构的更改可能会导致某些使用结构的过程失效。例如，如果我们对栈中的条目数量设置上限，可能会将底层结构改为：

```pascal
stack = record
  val : array [1..100] of integer;
  head_num : integer;
  end;
```

该方案的另一个局限性是它不允许根据结构中的其他项来定义字段项。例如，最好将员工定义为：

```pascal
employee = record
  name : a name;
  age : 1..80;
  wage : real;
  hours : real;
  pay : (wage * hours);
  end;
```

其中 `pay` 是一个只读字段，每次被访问时都会计算。

#### 1.3.2 面向对象的数据抽象

SIMULA67 [2] 允许定义一种更健壮的结构，被称为“类”（class）。类是由数据原语、过程、函数和其他类来定义的。类的定义类似于过程的定义，其中过程体（即类体）是用于初始化该类新对象的代码。假设 PASCAL 已经扩展到可以理解“类”（CLASSES），我们可以将栈的示例重写为：

```pascal
program reverse (input,output);

class stack;
  type
    stk_p = ^stk;
    stk = record
      val : integer;
      nxt : stk_p
    end;
  var
    s : stk_p;

procedure push (v : integer);
  var
    tmp_s : stk_p;
  begin
    tmp_s := s;
    new(s);
    s.^val := v;
    s.^nxt := tmp_s
  end;

function pop : integer;
  begin
    pop := s.^val;
    s := s.^nxt
  end;

function empty:boolean;
  begin
    empty := s = nil
  end;

begin {stack initialization}
  s := nil
end; {stack}
nvar s : stack; i : integer;
begin
  new(s);
  write('enter value ');
  while not eof do
    begin
      readln(i);
      s.push(i);
      write('enter value ')
    end;
  writeln('the reversed list is');
  while not s.empty do writeln(s.pop)
```

end.

栈的概念在两个程序中非常不同（尽管它们看起来非常相似）。在纯 PASCAL 程序中，我们通过 `push`（入栈）和 `pop`（出栈）来操作栈结构。在面向对象的方法中，我们向栈请求信息（`s.pop`）并向栈下请求操作（`s.push`）。正是这种将对象实例视为“黑盒”实体的观点，牢地将对象的底层结构从程序中隔离开来。此外，类/对象结构的某些实现 [7] 可以选择性地限制对象组件的“可见性”（例如数据结构或函数/过程）；这种功能在类似 PASCAL 的方案中是找不到的。

### 1.4 CADRS 简述

尽管 CADRS 并非真正的面向对象系统，但它实现了面向对象系统的许多优势。这是通过扩展更传统的结构定义方案实现的。以下对 CADRS 的总结将说明最后一点，并为读者在随后的比较分析中提供帮助。

`structure` 函数用于定义所有的 CADRS 结构。它的第一个参数是待定义的结构名称。剩余的参数被视为一系列属性/属性-值对，用于实例化该结构定义。

以下是有效的结构属性列表及其每个属性的描述：

- `TYPE`
  - `TYPE` 属性描述了应该用于实现所定义结构的底层 LISP 结构。允许的值有：
    - `list` - 用于列表。
    - `a-list` - 用于关联列表（association list）。
    - `p-list` - 用于分离属性列表（property list）。
    - `array` - 用于 MACLisp 风格的数组。
    - `hunk` - 用于块（hunk）。
    - `hash` - 用于哈希链（hash link）。
  - 如果未指定此属性，则假设值为默认列表。

- `FIELDS`
  - `FIELDS` 属性的值是要为该结构定义的数据项列表。

- `TO-CREATE`
  - `TO-CREATE` 属性的值是一个表达式，当其求值时将创建所定义结构的实例。这被用于覆盖 CADRS 计算出的格式。

- `BEFORE-CREATING`
  - `BEFORE-CREATING` 属性的值是在创建每个结构实例时都会被求值的形式。

- `AFTER-CREATING`
  - `AFTER-CREATING` 属性用于指定一个在结构实例创建后进行求值的形式。在评估 `AFTER-CREATING` 形式时，原子数据（atom datum）将绑定到创建的实例。

- `IS-A`
  - `IS-A` 属性允许结构继承一个或多个之前定义的结构的定义。

- `TYPECHECK`
  - `TYPECHECK` 属性用于告诉 CADRS 对该结构的所有创建实例进行类型检查。

- `TYPE?`
  - `TYPE?` 形式的值被视为一个 lambda 表达式或函数名，当对任意形式进行求值时，如果该形式是该结构的实例则返回 `t`，否则返回 `nil`。

字段与结构一样，也拥有属性，其值可以在结构定义期间赋值。1 有效的字段属性列表为：

- `IS-A`
  - `IS-A` 字段属性将字段定义为属性值所指的结构的实例。

- `TO-FETCH`
  - `TO-FETCH` 属性用于指定一个 lambda 表达式或“模式”2，该模式将返回一个表达式，用于从形式中获取字段的值。这被用于覆盖 CADRS 生成的格式。

1. 这种机制在 CADRS 参考章节中显示。
2. 例如 `(car)` 返回列表中的第一个元素。

# 1984年7月3日

- `TO-REPLACE`
  - `TO-REPLACE` 属性的值是一个 lambda 表达式或“模式”，该模式将返回一个表达式，用于从形式中替换字段的值。

- `DEFAULT`
  - `DEFAULT`（默认）属性的值是一个用于求值的表达式，用以给字段一个默认值。如果未指定此属性，则使用 `valuersDefault`。

- `TYPE`
  - 字段的类型定义了字段是实际占用空间，还是仅通过函数/过程定义。如果值为物理的（physical），则在底层结构中预留单元格；如果是虚拟的（virtual），则不留空间。

- `HASH-SIZE`
  - `HASH-SIZE` 属性仅适用于底层类型为 `hash` 的字段。该属性的值用于指定该字段哈希表的大小。

- `BEFORE-FETCHING`
  - `BEFORE-FETCHING` 属性用于指定在从形式中获取字段值之前求值的形式。求值期间，符号数据（symbol datum）绑定到执行 fetch的形式。

- `AFTER-FETCHING`
  - `AFTER-FETCHING` 属性用于指定在从形式中获取字段值后求值的形式。符号数据和值分别绑定到执行 fetch的形式和对应的值。

- `BEFORE-REPLACING`
  - 该属性的值对应于替换操作的 `BEFORE-FETCHING` 属性。符号数据和新值被绑定到相应的值。

- `AFTER-REPLACING`
  - `AFTER-REPLACING` 属性的值是在字段值替换后求值的形式。符号数据和新值被绑定到相应的值。

- `MUST-BE`
  - `MUST-BE` 属性的值是在每次替换字段值时都会求值的形式。在形式求值期间，符号数据和新值被绑定到相应的值。如果该形式返回，则执行替换；如果返回 `nil`，则发生错误。

`create` 函数用于创建结构的实例。除外，`create` 允许用户初始化结构的任何字段或子字段。

`fetch` 和 `replace` 函数提供了访问结构实例字段的功能。`fetch` 根据指定的路径返回字段的值，而 `replace` 将用新值替换字段的值。

#### 1.5.1 DEFSTRUCT

`DEFSTRUCT` 包装是一个结构定义工具，运行在 PDF10、Multics MacLisp 以及 LispMachines 上。它具有 CADRS 的许多功能并且是可以扩展的。

这两个包都为创建实例（instance）时所使用的底层 LISP 结构提供了多种选择。CADRS 对列表结构的实现略为强大，因为它允许用户指定列表的精确格式（通过嵌入子列表，以及使用 `cons` 单元格的最后一个 `cdr` 来存储值）。DEFSTRUCT 提供的选择是线性列表或平衡树。

DEFSTRUCT 方案的缺点是，字段（field，或者在 DEFSTRUCT 中称为槽位 slot）不能显式地声明为另一个结构的实例。这种差异在下面的示例所示。

```common
--CADRS 对 'name' 和 'person' 的定义
(structure name fields (last first . mi))
(structure person type array)
  fields ((declare name is-name) age sex))

(fetch a-person name first)

(create
  (age . 24) (sex . 'Male)
  ((name last) . 'Duncan) ((name first) . 'Richard
  ((name mi) . 'J))

--DEFSTRUCT 对 'name' 和 'person' 的定义
(defstruct (name (type list*))
  last first mi)
(defstruct (person (type array))
  name age sex)

(name (person a-person))

(make-person age 24 sex 'Male name 'Duncan Richard . J)
```

访问 person 结构中不同字段/槽位（以及子字段/子槽位）的方法是相同的。问题在于，DEFSTRUCT 无法得知 person 结构中的 `name` 槽位被定义为 `name` 结构。因此，该槽位必须初始化（使用列表），而不是初始化每个子槽位。如果 `name` 结构的底层发生变化（例如变为 `array`），这将成为潜在的问题源。

虽然两个包允许一个结构包含另一个的定义（CADRS 中的 `is-a` 结构属性和 DEFSTRUCT 中的 `include` 选项），但 DEFSTRUCT 版本灵活性小得多。`include` 选项只能用于具有特定底层类型的结构，并且只有槽位初始化表达式可以从其原始值更改。在 CADRS 中，任何结构或字段属性都可以被更改或修改，任何结构类型都可以被继承。

CADRS 提供的 `create` 函数支持由 DESTRUCT¹ 定义的 `make-x` 和 `alter-x` 宏的组合功能。此外，`create` 还支持许多其他特性（为了与 INTERLISP Record Package 兼容所需的特性），例如：

- `create` 可以被告知在创建实例时粉碎（类似 alter）、使用另一个结构的顶层结构，或复制另一个结构的顶层结构。

- `create` 保留了提供的任何字段初始化的求值顺序。为了说明这一点，考虑以下结构和 create 表达式：



```common
(structure test-init fields (a b c d e f))
(create test-init (e . 10) (f . 20) (d . 30) (b . 40) (c . 50) (a . 60))
```

满足给定求值顺序的评估形式为：

```common
((lambda ($ss $$f $$sd $$bb $$sc)
(list a $$bb $$sc $$sd $$se $$ff))
10 20 30 40 50)
```

- 其中 `x` 是当前定义的结构之一的。

`CADRS` 中的许多功能在 `DEFSTRUCT` 中无法直接使用，但理论上可以使用 `DEFSTRUCT` 的扩展能力来实现。这些特性列举如下：

- 当更改槽位值时，没有方法可以验证新的槽位值。
- 所有槽位名称必须是唯一的（即没有类型检查/typing）。
- 结构创建或槽位访问没有过程化挂钩。
- 不支持虚拟字段（槽位）。

由于 `CADRS` 的设计基于 `INTERLISP` Record Package (ILRP)，这两者有许多共同点。每个包支持的底层结构类型有很大的交集¹。用于实例创建和结构访问的函数在大多数情况下是相同的。

`ILRP` 可以指定局部于正在定义的结构²子结构——这种机制在 `CADRS` 当前版本中是不支持的。例如，可以这样定义一个消息：

```common
(record msg ((from . to) mess) (record msg (header . body)))
```

这提供了一种访问整个 `mess` 字段或其组件之一的方法，而无需定义单独的 `mess` 记录（这在 `CADRS` 中是要求的）。此外，`ILRP` 允许一个字段拥有多个这样的定义。

- 不集由无法在主机 `LISP` 中实现的类型组成。
- `ILRP` 结构被称为记录（records）。

这两个包都支持实例类型机制，尽管两者在实现方式上差异很大。`ILRP` 使用谓词确定形式的类型，谓词检查对象是否为实例。考虑以下：

```common
(record foo (a b c d) e)
```

为了确定 `x` 是否为的实例，基于网络使用：

```common
(and (listp x) (length x) (caddr x))
```

`CADRS` 不具备包含另一个定义的能力。这在某种程度上可以通过使用自定义类型来实现²。

- `INTERLISP` Record Package 是
- `is-a` 在 `CADRS` 中

`GLISP` 对象消息功能的某些方面可以在 `CADRS` 中通过 `replace` 函数结合 `to-replace` 字段属性来模拟。主要的局限性是消息只能有一个参数。运算符重载无法在重写必要的函数（以执行 `GLISP` 编译器的工作）。

`GLISP` 是一种基于 `LISP` 的强类型面向对象语言。该语言使用类似于英语的语法，并配备了启用基于对象的消息功能和路径确定能力的编译器。由于 `CADRS` 不是编程语言，而更像是一个工具，因此对比目的仅使用对象/结构定义。

通常，`CADRS` 与 `GLISP` 对象/结构定义相比良好。一个主要区别是 `GLISP` 结构和对象的强类型程度（这用于编译器推理）。

两者都具有构建结构类型层次的能力，并扩展结构类型的定义¹。每个都有复杂的挂钩机制，允许实现虚拟字段。

- `ACCESSFNS` 记录要求所有的结构访问和创建代码由用户提供。

## 1.6 CADRS 与表示方案

本节将 `CADRS` 与 `FRL` [5] 中体现的网络知识表示方案进行比较。这种比较的目的是既不是暗示 `CADRS` 在任何意义上都是知识表示工具，也不是提议将其此类使用。相反，目标是表征此类知识表示方案的描述能力，以洞察适用于数据结构描述的能力类型。为了方便读者进行比较，这里提供了关于网络方法的简短总结。

正如 `Mylopoulos` 在 [3] 中提到的，“对象（节点）和二元关联（标签边）来尝试描述一个世界，前者表示个体，后者表示被建模世界中的二元关系。”

在 `FRL`（帧表示语言）中，对对象的描述被称为“帧”（frame），与 `CADRS` 结构非常相似。帧的结构如下：

```
(frame
  (slot1
    (facet1
      (datum1 (label1 message1 message2 ...))
      (label2 message1...))
      (datum2 (label1 ...) ...) ...)
    (facet2 ...) ...)
  (slot2 ...) ...)
```

帧之间可以根据其 `AKO`（A Kind Of，一种）槽位的值按层级关系建立关联（例如，`DOG` 帧的 `AKO` 槽值可能是 `ANIMAL`），并且每个槽（`slot`）都可以被指定为一个帧（例如，`CAR` 帧包含一个 `WHEEL` 槽，而该槽也是一个帧）。每个槽可以有若干个面（`facet`）来描述它。面还可以用于指定过程的调用：

- 当槽位的值被更改或访问时。
- 为没有 `VALUE` 面的槽提供值。
- 为没有 `VALUE` 面的槽提供默认值。
- 验证槽位的值。

`FRL` 帧结构及其关联背后的许多思想已被引入到 `CADRS` 中。泛化（`FRL` 中的 `AKO` 和 `CADRS` 结构中的 `IS-A`）、聚合（将对象的各个定义为其他对象的能力）以及过程附加（`procedural attachment`）的概念在这两种描述中都是非常有用的。

根据类型对对象实例进行分类的能力同样有用。

`FRL` 和 `CADRS` 之间的许多差异源于各自方案的目标。例如，随着对对象知识的增长而向帧中添加新槽的需要，在结构定义领域是没有对应项的，因为结构通常是静态的。因此，`CADRS` 不提供向现有结构添加新字段的方法。此外，结构定义方案所支持的继承类型不需要像知识表示法那样具有动态性；这再次归因于结构定义是静态的假设。

如上文所示，`FRL` 帧中的每个槽除了系统理解的面之外，还可以包含用户定义的面。虽然 `CADRS` 属性仅限于系统定义的属性，但放宽这一限制以允许信息与结构/字段关联，似乎是非常值得的，且目前正在考虑中。

# 2 - CADRS 参考

## 2.1 引言

接下来的 10 章将深入处理 `CADRS` 的各种特性。如所述，这些章节旨在作为 `CADRS` 软件包 1.00 版本及其在 `Franz Lisp Opus 37` 下实现的参考手册。

## 3 - structure - 结构结构定义

`structure` 函数用于定义 `CADRS` 结构以及描述它们之间的相互关系。与 `INTERLISP`（或者说 `PASCAL`）一样，`structure` 不会创建被定义结构的实例。因此，不会返回相关值。与 `CADRS` 许多部分类似，`structure` 被实现为一个宏，该宏反过来使用低级函数来实际定义结构。

### 3.1 语法

`structure` 的语法为：

```
(structure attrib1 [mod1] vali attrib2 [mod2] val2 ..)
```

其中：

- `attrib1` 是可接受的结构属性之一（见下文）。
- `modi` 是该属性的可选修饰符¹。
- `vali` 是与该属性关联的值。

所有属性都是可选的。

> 1. 某些属性带有修饰符，用于指定其值如何被继承。属性修饰符将在“结构继承”章节中介绍。

### 3.2 结构属性

尽管所有结构属性（以及字段属性）都有默认值，因此不需要指定，但属性将取的实际值取决于结构的“血缘”（lineage）¹。虽然这一点在结构继承部分有更完全的阐述，但在这里应该指出，下文提到的默认值实际上受到了结构血缘的影响。

#### 3.2.1 type

`type` 属性的值指定了用于创建该结构实例的底层 `LISP` 结构。允许的值有：

- `list`（默认值）类型为 `list` 的结构中的字段以元素的形式存储在列表中。
- `a-list` 字段的值存储在关联列表（association list）中键 `<field>` 的值中（无论字段的名称是什么）。例如，如果一个结构有一个名为 `foo` 且值为 `bar` 的字段，以及一个名为 `dog` 且值为 `cat` 的字段，那么 `a-list` 可能如下：

```
((foo . bar) (dog . cat) . .)
```

- `p-list` 值存储在离散属性列表（disembodied property list）² 中指示符 `<field>` 的值中。如果上述字段和值在一个 `p-list` 结构中，它可能看起来如下：

> 1. 结构的血缘是已继承的结构集合，以及该集合中每个相应结构的血缘。
> 2. 离散属性列表是不作为符号的属性列表子部分被访问（引用）的列表。

```
(foo bar dog cat . ....)
```

- `array` 字段的值存储在映射到该字段的数组中。使用示例，它可能如下：

```
------+-------+
| bar |
+-------+
| cat |
```

- `hunk` 字段的值存储在映射到该字段的 `hunk` 中。使用示例，它可能如下：

```
{bar}
```

- `hash` `hash` 结构与其他结构大不同。一个主要区别是值存储在独立的空间中。`hash` 结构最重要的用途之一是扩展结构。以下示例说明了 `hash` 结构及其技术：

> 1. `hash` 结构将详细介绍。
> 2. 由于此示例使用了稍后描述的函数，现在可能值得跳过它，以后回来。

考虑以下结构：

```
(structure some-data type hunk
  fields ((declare f1-a foo)
  (declare f2-a bar)
  f3
  f4
  (declare f5-a foobar)
)
```

如果我们使用 `some-data` 实例构建了一个大型网络，然后发现需要添加字段 `f6`，不使用 `hash` 结构的唯一办法是从头开始。如果我们定义一个 `hash`：

```
(structure add-the-field type hash
  fields ((declare f6 default nil)))
```

那么所有的 `some-data` 实例现在都将有一个字段 `f6`，因为对于任何实例 `sd`：

```
(replace sd f6 100) => (putash sd 100 f6)
```

（`f6` 是使用的数组）。

> 1. 即使 `some-data` 是列表，也有必要为该字段 `cons` 额外的空间。

#### 3.2.2 fields

`fields` 属性定义了组成被定义结构的不同数据项。`fields` 属性的默认值为 `nil，意味着“无字段”。

`fields` 的值称为字段列表，是结构中的字段列表。该列表有两个用途。第一个显然是定义字段。第二个是定义字段在任何 `list`、`array` 或 `hunk` 结构中的位置。对于 `list` 结构，此列表可以包含子列表，用于定义顶级结构中的嵌入列表。作为结构定义，每个字段具有关联修饰符和值的属性。这些规范将在后续章节讨论。

##### 3.2.2.1 示例

以下示例展示了不同结构如何处理不同的字段列表。

- `(structure name type list fields (last first mi))`

如果 `foo` 是 `name` 结构的实例，那么：

```
(car foo) => last
(cadr foo) => first
(caddr foo) => mi
```

- 为了兼容性，所有类型都允许嵌入字段列表。对于 `list` 以外的类型，字段列表的处理方式类似于线性的。
- 如果名称结构（在上例例中）的类型为 `a-list`，那么：

```
(cdr assq 'last foo) => last
(cdr assq 'first foo) => first
```

- 如果 `name` 的类型为 `hunk`，那么：

```
(cxr 0 foo) => last
(cxr 1 foo) => first
```

- `(structure bar type list fields ((a b) ((c) d) . e))`

如果 `foo` 是 `bar` 的实例，那么：

```
(caar foo) => a
(caadr foo) => c
(cddr foo) => e
```

- 如果 `bar` 的类型为 `array`，那么：

```
(funcall foo 0) => a
(funcall foo 3) => c
(funcall foo 5) => e
```

#### 3.2.3 创建相关属性

以下属性控制了在创建结构实例时会发生的情况。

##### 3.2.3.1 to-create

`to-create` 属性用于向 `create` 函数建议如何创建正在定义的结构实例。该属性的值是一个表达式，在求值时会返回该结构的实例。默认情况下，结构函数会构建这样一个表达式，在大多数情况下，该表达式的效率至少与用户定义的表达式相当。

下面的示例展示了如何使用 `to-create` 属性：

```
(structure name type list
  fields (last first mi)
to-create (list nil nil nil))
```

当调用 `create` 来创建一个名称时，它将求值表达式 `(list nil nil nil)`，结果返回 `(nil nil nil)`。

##### 3.2.3.2 before-creating

`before-creating` 属性的值是一个在创建结构实例之前要被求值的表达式。默认情况下，不会生成此类表达式。

如果如例所示使用 `before-creating`：

```
(structure foo
  fields (a b c)
  before-creating (bar))
```

那么 `create` 将返回一个类似于下面的表达式的结果：

```
(progn
  (bar)
  <<create-form>))
```

其中 `<create-form>` 是将创建实例的表达式。

##### 3.2.3.3 after-creating

`after-creating` 属性指定了一个在结构实例创建后求值的表达式。默认情况下，不会生成此类表达式。

创建的实例将绑定到原子 `datum`，该原子可以在表达式中被引用。此功能对于跟踪实例和/或在实例创建后对其进行修改非常有用。例如，当如下所示的结构：

```
(structure foo
  fields (a b c)
    after-creating (progn
      (print datum)
      (terpri)))
```

被创建时，`create` 将求值一个类似于下面的表达式：

```
(let ((datum <<create-form>))
  (progn
    (print datum)
    (terpri)))
```

#### 3.2.4 结构类型检查

以下属性控制 `CADRS` 如何确定结构实例的类型。

##### 3.2.4.1 type?

`type?` 属性用于告诉 `CADRS` 如何识别一个 `LISP` 实体是否为正在定义的结构实例。尽管 `CADRS` 可以进行结构类型检查，但该功能仅适用于使用 `create` 函数创建的实例。`type?` 属性对如何实现“类型检查”提供了更大的控制。

`type?` 属性的值是一个 `lambda` 表达式或接受一个参数的函数，如果参数是正在定义的结构的实例，则返回 `t`，否则返回 `nil`。以下是 `type?` 的使用示例：

```
(structure name type list
fields (last first mi)
type? name-type?)

defun name-type? (struct)
  (and dtpr struct)
  (eq (length struct) 3))
```

##### 3.2.4.2 typecheck

`typecheck` 属性用于引导 `CADRS` 对结构的所有实例进行类型检查。默认情况下，只有当结构包含一个字段，其定义与另一个结构中同名字段定义冲突时，才会对该结构开启类型检查。

如果 `typecheck` 的值为 `t`，则 `CADRS` 将对结构的所有实例进行类型检查。

`CADRS` 生成的类型检查和用户提供的类型检查表达式（`type?` 的值）都可以对某个结构开启。这样做的原因是允许类型检查在多个层级上进行。这一概念在随后的章节中会有详细解释。

#### 3.2.5 is-a

`is-a` 属性允许结构继承一个或多个之前定义的结构的定义。该属性受到限制，它必须作为调用 `structure` 时第一个使用的属性。

如果 `is-a` 属性的值是一个原子，则该结构将继承由原子命名的结构的定义。如果值是一个列表，则列表中的每个原子都被视为之前定义的结构，它们的定义将按照它们指定的顺序被继承。

`is-a` 的作用在“结构继承”章节中得到了完全介绍。

# 4 - 字段定义

`CADRS` 使用与结构级级别相同的相同属性/属性值语法，对结构的字段级定义提供了高程度的控制。本章提供了特定于字段列表（`field` 属性的值）的字段声明细节，以及指定字段属性的机制。

## 4.1 字段列表规范

通常情况下，字段列表是任何满足以下条件的有效列表：

- 列表中的每一项（字段）在结构内部内是唯一的。
- 列表是非环的（即它是会终止的）。

以下是有效字段列表的示例：

1. `(a b c)`
2. `(a . b)`

第一个示例显示了一个典型的字段列表。在第二个示例中，字段 `a` 将映射列表的 `car`（假设结构类型为列表），而字段 `b` 将映射列表的 `cdr`。在第三个示例中，点用于在列表中预留空间（类似于 `COBOL`）。

- 1. 与结构属性一样，某些字段属性可以指定这些属性如何被继承。字段属性在“结构继承”章节中介绍。

1984年7月3日

`(b c) . d)`

## 4.3 字段属性

未指定属性时，属性的实际值取决于结构的血系。以下字段属性控制 `CADRS` 如何执行字段访问以及对该过程的“自定义”。默认情况下，`CADRS` 为每个字段计算访问和存储函数。



这些函数通常与下面描述的 `to-fetch` 和 `to-replace` 字段属性配合使用以增强过程。

### 4.3.3 fetch 和 replace 定义

用于返回字段值和向字段存值的 CADRS 函数分别是 `fetch` 和 `replace`。

#### 4.3.3.1 to-fetch

`to-fetch` 字段属性的值可以是两种形式之一。如果是一个 lambda 表达式，CADRS 假设当对 `fetch` 中指定的结构实例进行求值时，它将返回获取字段的正确表达式，类似于宏体。默认情况下，CADRS 生成此形式：

```lisp
(structure a-structure
    fields ((declare a
        to-fetch (lambda form) (list 'car form))))
```

如果调用 `fetch` 来获取结构实例 `s` 的字段，如下：

```lisp
(fetch s a)
```

lambda 将带参数 `s` 进行求值并返回：

```lisp
(car s)
```

如果表达式不是 lambda，CADRS 假设它被用于“展示” CADRS 如何从结构实例获取字段。例如，考虑以下结构：

```lisp
(structure a-structure
    fields ((declare a to-fetch (cdr datum))))
```

`to-fetch` 字段属性值中的原子 `datum` 指导 CADRS 插入此处正在获取的结构实例。因此，如果评估了获取 `(fetch s a)`，CADRS 将评估表达式 `(cdr s)` 以执行获取。

#### 4.3.3.2 to-replace（替换）

`to-replace` 字段属性对应于在字段中存储值时所使用的 `to-fetch`。与 `to-fetch` 类似，该属性的值可以是一个 lambda 表达式，也可以是一个表达式。然而，在这种情况下，lambda 必须接受两个参数；第一个是要执行替换的操作的形式，第二个是用于替换旧值的新值。接下来的示例展示了如何操作：

```lisp
(structure struct
  fields ((declare a
    to-fetch (lambda (form val))
    (list 'replace form val))))
```

```lisp
(replace a-struct-instance 'this-new-value)
  --评估为--
```

```lisp
(replaced a-struct-instance 'this-new-value)
```

与 `to-fetch` 一样，如果表达式不是 lambda，CADRS 假设它将用于“展示” CADRS 如何替换结构实例中字段的值。与之前一样，如果 CADRS 在表达式中找到原子 `datum`，它将被替换为正在执行替换的结构实例。同样，如果 CADRS 在表达式中找到原子 `newvalue`，它将被替换为调用 `replace` 时指定的值。下文展示了这是如何发生的。

```lisp
(structure struct
  fields ((declare a
    to-fetch (replace datum newvalue))))
(replace asi asi 10) => (replace asi 10))
```

#### 4.3.3.3 before-fetching（获取前处理）

`before-fetching` 字段属性的值是在对字段执行获取之前要评估的形式。默认情况下，没有此类形式被评估。CADRS 将在一个上下文中评估表达式，在该上下文中结构实例被 lambda 绑定到 `datum`。下例展示了一个示例：

```lisp
(structure struct
  fields ((declare a
    before-fetching (note-fetch 'a datum)))

  (fetch as a)
  --将评估为 as-
  (let ((datum))
    (note-fetch 'a datum)
    (car datum)))
```

在示例中，`note-fetch` 可能被视为某个记录获取实例的函数。

#### 4.3.3.4 before-replacing（替换前处理）

`before-replacing` 字段属性的值是在对字段执行替换之前要评估的形式。默认情况下，没有此类形式被评估。该表达式在一个上下文中评估，其中结构实例和要替换当前字段的值分别被 lambda 绑定到 `datum` 和 `newvalue`。下例展示了一个示例。

```lisp
(structure struct
  fields ((declare a
    before-replacing
    (note-replace
      'a
      datum
      newvalue))))
```

```lisp
(replace asi a 10)
--将评估为--
```

```lisp
(let ((datum asi) (newvalue 10))
  (note-replace 'a datum newvalue)
  (rplaca datum newvalue))
```

在示例中，`note-replace` 可能被视为某个记录替换实例的函数。

#### 4.3.3.5 after-fetching（获取后处理）

`after-fetching` 字段属性的值是在从形式中获取值后要评估的表达式。默认情况下，获取形式是最后一个被评估的表达式。CADRS 将正在执行获取的结构实例和获取到的值分别 lambda 绑定到 `datum` 和 `value`，如下所示：

```lisp
(structure str
  fields ((declare a
    after-fetching (foo datum value))))
```

```lisp
(fetch a-str a) => (
  ((datum a-str)
  (value (car datum))
  (foo datum value)
  value))
```

#### 4.3.3.6 after-replacing（替换后处理）

`after-replacing` 字段属性的值是在形式中字段值替换后要评估的表达式。默认情况下，替换形式是最后一个被评估的表达式。CADRS 将 `datum` 和 `newvalue` 绑定到显而易见的值，如下所示：

```lisp
(structure str
  fields ((declare a
    after-replacing (foo datum newvalue)))

  (replace a-str a 10) => (let
    ((datum-str)
    (newvalue 10)
    (%%ret (rplaca datum newvalue))
    (foo datum newvalue)
    %%ret))
```

### 4.3.4 type（类型）

`type` 属性的值决定了结构内部是否为字段分配存储。如果 `type` 的值为 `physical`（物理的，默认值），则将为字段分配一个存储单元（例如列表结构中的列表单元格）。如果值为 `virtual`（虚拟的），则不分配存储。

当字段根据结构内部的其他字段进行定义时，此功能非常有用，例如：

```lisp
(structure employee
  fields ((declare name is-a-name)
    wage
    hours-worked
    (declare type
      virtual)))
```

如果如上所示的 `employee` 实例 `wage` 为 10，`hours-worked` 为 20，那么调用：

```lisp
(fetch wage)
```

将返回 10。要注意，如果字段是 `virtual`，则不分配存储。

#### 4.3.4.1 must-be（强制检查）

`must-be` 属性的值提供了检查合法性的手段。默认情况下不进行此类检查。该表达式在一个上下文中评估，其中结构实例和要检查的值分别被 lambda 绑定到 `datum` 和 `newvalue`。下例展示了一个示例：

```lisp
(structure student
  fields ((declare name is-a-name)
    wage
    hours-worked
    (declare must-be
      (check datum newvalue))))
```

```lisp
(replace student 99)
--评估为--
```

```lisp
(let ((datum student) (newvalue 99))
  (must-be 'grade newvalue)
  (rplaca datum newvalue))
```

在示例中，`must-be` 可能被视为某个记录替换的函数。

#### 4.3.4.2 hash-size（哈希大小）

`hash-size` 属性的值指定了 CADRS 为字段分配的数组。对于类型为 `hash` 的字段有意义。

# 5 create 创建结构

`create` 函数用于创建一个结构实例。它的语法与 `structure` 函数相似，保持了相同的灵活性，并包含以下功能：

- 为所有字段提供初始值。
- 创建另一个结构的副本。
- 在创建时使用结构实例。
- “重新初始化”结构实例。

除了上述之外，使用 `create` 的另一个原因是允许结构的基础类型发生变化（例如变为 `hunk`），而无需更改任何使用它的函数。

## 5.1 语法

`create` 的语法为：

> 1. 显然，如果不使用 `fetch`、`replace` 以及 `to-fetch`/`to-replace` 表达式，这将不成立。

```lisp
(create structure
[cr-attrib struc-instance]
  [(field-name1 . expr1)]
  [(field-name2 . expr2)]
  .
  [(field-namen . exprn))
```

其中：

- `structure` 是要创建的结构实例名称。
- `cr-attrib` 或创建属性，是 `using`、`copying` 或 `smashing` 之一。创建属性是互斥。也就是说，具有使用属性的 `create` 不能有复制属性等。创建属性的值是在创建过程中使用的结构实例。创建属性见下文。
- `field-namen` 是要初始化为 `exprn` 的字段名称。字段初始化见下文。

## 5.2 创建结构的注意事项

在创建结构时，应注意以下几点：

1. 创建的结构和被“使用”的实例结构类型必须相同。这是 1.00 版本的局限性。
2. 当字段赋予初始值时，就像该字段的默认属性是指定的值一样。因此，如果字段具有 `to-fetch`、`before-fetching`、`after-fetching` 或 `must-be` 属性，它们的影响在此时会被忽略。

## 5.3 字段初始化

当 `create` 遇到一个 (字段 . 表达式) 对时，表达式的值被用作字段的初始值。考虑以下结构定义和创建调用：

```lisp
(structure team
  fields (name town coach standing))

(create team
  (name . 'Eagles)
  (town . 'Philadelphia)
  (coach . 'Vermeil)
  (standing . 1))
```

`create` 实际上会求值的形式为：

```lisp
(list 'Eagles 'Philadelphia 'Vermeil 1)
```

CADRS 注意字段求值的指定顺序，以确保任何表达式在求值时产生的副作用都能产生“预期”的效果。考虑以下示例：

```lisp
(let ((na 'Cowboys) (to nil)
  (co 'Landry) (st 2))
  (create team
    (name . prog2)
    (coach . (setq to 'Dallas)
      co))
  (town to)
  (standing . st)))
```

这次，`create` 的求值方式为：

```lisp
((lambda ($coach))
  (list na to $coach st)
(prog2
  (setq to 'Dallas)
  co))
```

要初始化嵌套结构的字段，路径是通过一个列表作为字段名（而不是原子体）来指定的。例如，考虑以下结构：

```lisp
(structure name fields (last first . mi))
(structure person fields ((declare name is-a name)))
```

要初始化 `person` 结构的最后一个字段，应使用以下 `create` 表达式：

```lisp
(create person ((name last) . 'Smith'))
```

## 5.4 create 属性

在说明使用（`using`）、重用（`reusing`）、复制（`copying`）或粉碎（`smashing`）属性之间的区别，我们将考虑以下结构：

```lisp
(structure foo
fields (a b c d e))
```

其实例为：

```lisp
foo_inst <= (10 15 (20 25) 30)
```

### 5.4.1 using

`using` 属性会使 `create` 使用指定实例的顶层结构来创建新实例。因此，在如下 `create` 调用中：

```lisp
(create foo using foo-inst (a . 100) (c . 200))
```

`create` 将生成：

```lisp
list 100
(cadr foo-inst)
(list 200 (cadaddr foo-inst))
(cadddr foo-inst))
```

如果结构具有任何子结构，例如：

```lisp
(structure person fields ((declare name is-a name))
```

`create using` 将将子结构（类似于 `create copy`）复制到结构实例中。

### 5.4.2 reusing

`reusing` 属性使 `create` 在创建新实例时尽可能多地使用提供的实例。`create` 语句：

```lisp
(create foo reusing foo-inst (b . 150))
```

其求值结果为：

```lisp
(cons
(car foo-inst)
(cons 150)
(cddr foo-inst))
```

> 1. CADRS 的 V1.00 版本将不支持 `reusing`。如果指定了 `reusing`，结构将以 `using` 的方式创建。

### 5.4.3 copying

`copying` 属性引导 `create` 使用 `copy` 函数复制实例中的顶层项。因此：

```lisp
(create foo copying foo-inst (d . 250))
```

其求值结果为：

```lisp
(list (copy (car foo-inst))
(cadr foo-inst))
(list (copy (caaddr foo-inst))
250)
(copy (caddr foo-inst)))
```

### 5.4.4 smashing

`smashing` 属性使 `create` 通过粉碎结构来执行创建，所示：

```lisp
(create foo smashing foo-inst (a . 100) (b . 150))
```

```lisp
(let ((f foo-inst))
(rplaca foo-inst 100)
(rplaca (cdr foo-inst) 150))
f)
```

# 6 结构访问函数

本章描述了 `fetch`/`val-of` 和 `replace`/`val-to` 函数，它们执行了 CADRS 中所有用户级别的结构访问。与结构和 `create` 函数一样，所有的结构访问函数都实现为宏，在适当的模式下可以替换为用于求值的代码。

## 6.1 fetch 和 val-of

`fetch` 和 `val-of` 函数返回结构实例中字段的值。每个者的语法如下：

```lisp
(fetch stru-inst path-spec)
(val-of stru-inst path-spec)
```

其中：

- `struct-inst` 是执行 `fetch` 的结构实例。
- `path-spec` 是指定字段的路径规范。



#### 6.1 fetch 和 val-of

其中：

- `struct-inst` 是执行 `fetch` 的结构实例。
- `path-spec` 是指定字段的路径规范。

要初始化嵌套结构的字段，路径是通过一个列表作为字段名（而不是原子体）来指定的。例如，考虑以下结构：

```scheme
(structure name fields (last first . mi))
(structure person fields ((declare name is-a name)))
```

要初始化 `person` 结构的最后一个字段，应使用以下 `create` 表达式：

```scheme
(create person ((name last) . 'Smith))
```

#### 6.2 replace 和 val-to

`replace` 和 `val-to` 函数对应于 `fetch` 和 `val-of`，用于在结构中修改或获取字段信息。每个者的语法如下：

```scheme
(replace stru-inst path-spec new-val)
(val-to stru-inst path-spec)
```

其中：

- `stru-inst` 是要修改的结构实例。
- `path-spec` 是指定字段的路径规范。
- `new-val` 是要设置的新值。

与 `fetch` 和 `val-of` 类似，`replace` 在存在时使用 `to-replace` 形式，而 `val-to` 则总是使用 CADRS 生成的形式。

# 7 - type and type?

`type` 和 `type?` 函数提供关于结构类型的信息。虽然这两者更有趣的应用将在下一章“结构继承”中讨论，但它们的功能将在在此介绍。

#### 7.1 type

`type` 的语法为：

```scheme
(type struc-inst)
```

其中：

- `struc-inst` 是某个结构的实例。

`type` 返回的值是 `struc-inst` 实例的一个或多个结构列表。例如：

```scheme
(structure s1
fields (a b c)
typecheck t)

(type create s1)) => (s1)

(structure s2 is-a s1)

(type create s2)) == (s2 s1)
```

使用 `type` 必须开启结构的类型检查。

#### 7.2 type?

`type?` 是一个谓词函数，如果其第一个参数是第二个参数中一个或多个结构的实例，则返回 `t`，否则返回 `nil`。

`type?` 的语法为：

```scheme
(type? struc-inst struc-list)
```

其中：

- `struc-inst` 是某个结构的实例。
- `struc-list` 是以下之一：
  - 之前定义的结构。
  - 之前定义的结构列表。

为了让 `type?` 正常工作，`struc-list` 中的每个成员（或单个结构）必须满足以下条件之一：

1. 隐式或显式指定了类型检查（使用 `type?` 结构属性）。
2. 已指定了 `type?` 形式。如果都不满足这些条件，将调用 `type?` 异常处理器。

1984年7月3日

生成的表单。

#### 7.3 通用类型化

CADRS 执行的结构类型化（structure typing）是非常直接的。然而，更改类型（`type?`）结构属性和函数的机制为实现更复杂的类型概念提供了手段。

例如，给定 `person` 结构的定义如下：

```scheme
(structure person
fields ((declare name is-a name)
age
sex))
```

我们可以定义一个“女性（women）”的概念为：

```scheme
(structure women
type?
(lambda (s)
  (and (memq 'person (type s))
    (eq (fetch s sex) 'female))))
```

并发现：

```scheme
(type? (create person (sex . 'female)) (women))
```

实际上会返回 `t`。

此外，使用 CADRS，可以定义一个全局类型处理程序来处理所有对 `type?` 的请求，从而为实例类型化提供了额外的粒度。这种技术在“异常处理”章节中进行了介绍。

1984年7月3日

# 8 - 结构继承

作为后续内容的引言，这里介绍的结构继承方式并非知识表示语言（FRL, KRL, KL-ONE）中所那种类型。考虑到 CADRS 属性大部分程度上是指令性的而非描述性的，且属性集是固定的，这可能是显而易见的。从积极的一方面来看，结构继承确实超越了其他结构定义工具（INTERLISP Record Package 或 MacLISP 的 `DefStruct`）提供的功能，它提供了一种扩展和修改结构定义的手段，以创建与父结构语义上相关的新定义。作为此类功能用性的示例，请考虑以下内容。

1984年7月3日

注意以下用于处理学生和员工信息的结构：

```scheme
(structure student
  fields ((declare name is-a name)
    (declare address is-a address)
    ss-number
    sex
    age
    school
    major
    courses
    advisor
    date-of-grad))
```

```scheme
(structure employee
  fields ((declare name is-a name)
    (declare address is-a address)
    ss-number
    sex
    age
    manager
    division
    group
    wage
    hours
    ytd-hours))
```

1984年7月3日

显然，两者之间存在一个共同的信息内核。在概念层面上，这无疑是因为学生和员工都是人。为了在 CADRS 中捕捉这种关系，可以根据 `person` 的定义来定义 `student` 和 `employee`，例如：

```scheme
(structure person
  fields ((declare name is-a name)
    (declare address is-a address)
      ss-number
    sex
    age))

(structure student is-a person
  fields (school
    major
    courses
    advisor
    date-of-grad))

(structure employee is-a person
  fields (manager
    division
    group
    wage
    hours
    ytd-hours))
```

两种方法（带有和不带 `'person'`）都提供了相同的结构访问（从 `fetch` 或 `replace` 的角度来看），从这个意义上说，继承机制仅仅提供了一种方便的简写符号。在实例类型化（instance typing）方面，第二种方法允许用户在两个粒度级别检查人/员工实例的类型（例如，`x` 是否是一个人，或者 `x` 是否是一个学生）。

本章的前半部分描述了结构和字段属性被继承的方法。随后是关于实例类型继承语义概念的讨论。

属性修饰符按限制程度从高到低依次为：`only`（仅）、`always`（总是）和 `also`（也）。这些对属性值的影响取决于父级上指定的修饰符。以下描述了修饰符及其影响：

1984年7月3日

1. `only`。这种唯一修饰符禁止结构的任何后代类修改属性值。只要父结构中的属性是使用 `also` 修饰的，就可以在后代类中使用 `only`（即：如果父属性使用 `only` 或 `always` 修饰，则会导致错误）。如果后代结构中使用了 `only` 这种修饰符，则被继承的属性值将由指定的值覆盖，且该层级的修饰符将变为 `only`。

2. `always`。这是限制性第二大的修饰符。`always` 只能通过 `also` 修饰符进行修改。当 `always` 被继承并被 `also` 修改时，当前值将进行拼接<sup>1</sup>。当 `also` 被继承并被 `always` 修改时，值将拼接且修饰符将变为 `always`。

3. `also`。这是限制性最低的修饰符。当一个可修改属性未指定修饰符时，默认使用 `also`。当 `also` 被继承时，其值会被 `only` 覆盖，并在 `also` 和 `always` 处进行拼接。修饰符将变为后代结构所指定的那个。当后代结构中对 `always` 和 `also` 的指定为 `also` 时，值将拼接且修饰符保持不变。

最后，虽然可修改属性不一定指定修饰符，但如果为不可修改的属性给出修饰符，将会导致错误。

注意，不可修改的属性隐地为 `only`。

<sup>1</sup> 值拼接或分组的方式取决于涉及的属性。下文将对此解释。

1984年7月3日

下面的图显示了允许的组合：

| | `only` | `always` | `also` |
| --- | --- | --- | --- |
| `only` | ERROR | ERROR | concat |
| `always` | ERROR | `always` | concat |
| `also` | concat | concat | concat |

1984年7月3日

#### 8.1.2 结构属性

以下描述了结构属性是如何被继承的。结构属性连同其值的继承方式如下。

1984年7月3日

##### 8.1.2.1 type

在 CADRS 1.0 版本中，`type` 是不可修改的属性，因此在未来的版本中可能会放宽限制。

1984年7月3日

##### 8.1.2.2 fields

`fields` 的值可以被后代类修改，其拼接方式通过以下示例说明：

```scheme
(structure s1
  fields (a b))

(structure s2
  fields (d e))
```

`fields` 的拼接结果为：

```scheme
(a b d e)
```

1984年7月3日

##### 8.1.2.3 before-creating and after-creating

这二类属性在继承时都使用标准语法。拼接方法是将形式按顺序插入 `create` 表达式中：

```scheme
(structure s1
  fields (a b)
  before-creating (foo)
  after-creating (bar))

(structure s2 is-a s1
  fields (a b)
  before-creating (s2foo)
  after-creating (s2bar))

(create s2) => (progn
  (foo)
  (s2foo)
  (let ((datum (list nil nil))
    (bar)
    (s2bar))
  datum))
```

1984年7月3日

#### 8.1.3 to-create type? and typecheck

`to-create`、`type?` 和 `typecheck` 属性是不可修改的。

#### 8.1.4 字段属性

字段属性的继承实现方式与结构属性的继承相似。每个字段属性的继承细节如下。

1984年7月3日

##### 8.1.4.1 default-is-a-to-fetch-to-replace type

`default-is-a-to-fetch-to-replace` 和 `type` 字段属性是不可修改的，后代类尝试更改继承的值会导致错误。

1984年7月3日

##### 8.1.4.2 before/after/fetching/replacing

`before-fetching`、`after-fetching`、`before-replacing` 和 `after-replacing` 使用标准语法进行修改。拼接方法是将形式按顺序插入 `fetch`/`replace` 表达式中，所示：

```scheme
(structure s1
  fields ((declare a
    before-fetching (foo)
    after-replacing (bar newvalue))))

(structure s2 is-a s1
  fields ((declare a
    before-fetching (s2foo)
    after-replacing (s2bar newvalue)))))

(replace an-s2 10) => let
  ((datum an-s2)
    (newvalue 10)
    (%ret (rplaca datum newvalue)
      (bar newvalue)
      (s2barvalue))
    %ret))
```

1984年7月3日

##### 8.1.4.3 must-be（必须满足）

`must-be` 属性可以使用标准语法进行修改。使用的拼接用于将值放入队列，然后在生成 `replace` 函数时，如下所示将这些值“与”（`and`）逻辑连接在一起：

```scheme
structure s1
    fields ((declare a
        must-be (evenp newvalue)))

structure s2 is-as sl
    fields ((declare a
        must-be (< 10 newvalue)))

replace an-s2 a 20) => rplca
    an-s2
        let ((newvalue 20))
        cond
            ((and (evenp newvalue)
                (< 10 newvalue))
                newvalue)
            (t (must-be-handler
                a
                    newvalue
                '(s1 s2)
                an-s2))))
```

### 8.2 继承与类型

结构继承（Structure Inheritance）对类型的影响取决于 `type` 函数的返回值。对于一个顶层结构，例如：

```scheme
(structure level-1 ...)
```

1984年7月3日

对 `type` 的调用如下：

```scheme
(type (create level-1))
```

返回一个其唯一成员为 `level-1` 的列表。对于下一层：

```scheme
(structure level-2 is-a level-1 ...)
```

对 `type` 的调用如下：

```scheme
(type (create level-2))
```

将返回一个包含 2 个元素的列表，第一个是该形式所属的结构名称，第二个是该结构的父结构。

通常，`type` 返回的值是一个结构列表：

```scheme
(struct1 stru2 . . strucn)
```

其中 `struct1` 是该形式的结构类型，对于列表尾部的每个 `struci`，`struci` 是某些 `strucj` 的父结构，其中：

```
1 <= j < i
```



# 9 - 运行模式

CADRS 许多功能具有两种或两种不同的运行模式。这些模式要么由用户显式设置，要么由 CADRS 根据定义的不同结构之间的关系设置。本章将涵盖不同的运行模式，解释如何显式设置它们，并描述 CADRS 自身更改模式的条件。

## 9.1 宏替换

如果符号 `cadrsReplaceFlag` 的值设置为 `t`，则所有对用户级函数的调用都将使用 `rplaca` 和 `rplacd` 将自身替换为它们的展开 1。默认情况下，该符号的值为 `nil`，不进行任何替换。

当然，如果效率是主要的考虑因素，最好的做法是编译所有函数和宏。然而，由于许多系统在最终编译之前会在解释模式运行一段时间，此功能将节省大量的内存，特别是在处理复杂结构时。

此功能必须由用户显式设置。

- 1. 记住所有顶层函数都是作为宏编写的。

## 9.2 类型化

通常情况下，CADRS 仅在以下情况生成实例类型代码：

- 1. 当结构定义中 `typecheck` 结构属性的值被显式设置为 `t` 时。
- 2. 当两个或多个结构包含对同一字段的冲突定义时。在这种情况下，CADRS 将强制将每个结构的 `typecheck` 值设置为 `t`。

通过将符号 `cadrsTyping` 的值设置为 `t` 可以开启所有结构的类型检查。该符号的默认值为 `nil`。

## 9.3 路径检查

CADRS 能够检查指定的获取/替换类型函数的路径是否正确。要做到这一点，必须同时开启类型检查（即符号 `cadrsTyping` 必须设置为 `t`），并且符号 `cadrsPathCheck` 的值必须设置为 `t`。此功能必须显式开启，且默认关闭（值为 `nil`）。

# 10 - 异常处理

CADRS 处理异常（错误）的方法与 Franz Opus 37 中带有 INTERLISP 扩展的方法类似，这使得编写异常处理程序的工作不那么困难¹。异常处理算法为：

- i. 检查是否存在针对该类错误的异常处理程序。如果没有，则跳转到步骤 iii。
- ii. 使用该类错误的参数调用所有用户指定的异常处理程序。如果任何一个程序返回了非 `nil` 列表，则返回列表的第一个元素作为继续处理的值。
- iii. 如果没有异常处理器“处理”该错误（或未指定任何处理器），则调用该类错误的默认错误处理程序。

## 10.1 CADRS 异常

以下描述了 CADRS 1.00 版本中实现的不同异常或可恢复错误。每个异常都与其传递给任何异常处理函数的参数一起给出。

### 10.1.1 cadrs-except-must-be

当结构中字段的 `must-be` 测试失败时，发生此异常。该错误的所有异常处理程序必须接受以下参数：

> ¹ 异常处理没有深度绑定 Franz 错误处理系统，以便将 CADRS 移植到其他 LISP 系统。Franz 错误系统仅在最低底层使用，以便调试错误。

- 1. 引起异常的字段名称。
- 2. 引起异常的值。
- 3. 结构实例。
- 4. 正在执行的函数（`val-of` 或 `val-to`）。
- 5. 失败的形式。

如果处理程序返回了非 `nil` 列表，则取列表的第一个元素作为继续处理的值。

### 10.1.2 cadrs-except-type

当一个多个结构包含同一字段的冲突定义时，产生此异常。在这种情况下，CADRS 将强制将每个结构的 `typecheck` 值设置为 `t`。

- 1. 引起异常的字段。
- 2. 引起异常的值。
- 3. 结构实例。
- 4. 正在执行的函数（`val-of` 或 `val-to`）。
- 5. 失败的形式。

如果处理程序返回了非 `nil` 列表，则取列表的第一个元素作为继续处理的值。

### 10.1.3 cadrs-except-nfft

`nfft` 异常在以下条件下发生：

- 1. 对结构执行了 `val-of` 或 `val-to`。
- 2. 类型检查开启。
- 3. 结构不包含该字段。

如果处理程序返回了非 `nil` 列表，则取列表的第一个元素作为继续处理的值。

## 10.2 异常处理器

通过 `establish` 函数在 CADRS 中激活或挂载异常处理器。语法为：

```
establish exception-name handler
```

其中：

- `exception-name` 是异常名称（如上所述）。
- `handler` 是 lambda 或一个绑定为处理该类型的 lambda 的符号。

在此时，`establish` 只是将函数名或 lambda 放入作为 `exception-name` 值的列表中。使用 `establish` 以保持系统与未来版本的向上兼容性。

## 10.3 异常处理器示例

以下演示了如何为某些类型的异常编写异常处理器。

### 10.3.1 cadrs-except-must-be 示例

应用是构建一个结构，它会提示 "yes" 或 "no"，并分别返回 `t` 或 `nil`。

```scheme
(structure yes-no
  fields ((declare answer
            to-replace (memq newvalue)
                  '(Y y yes YES)
            must-be (memq newvalue)
                  '(Y y Yes YES)
                  N n ho no NO))))

(defun yes-no-handler (field value type)
  (if memq 'yes-no type
      then do ((newvalue prog2
                    (msg N)
                    "Invalid answer"
                    N
                    "Answer yes or no : "
                    (read))
            ((test) (ncons newvalue))
      (else nil))

(establish cadr-except-must-be 'yes-no-handler)
```

注意以下点：

- 1. 如果异常处理器设计用于处理特定结构、字段或结构/字段组合的异常，它必须检查第一个和第三个参数（字段和类型）的值，以确定异常是针对该类型生成的。如果不是如此，处理程序应如所示返回 `nil`。
- 2. 处理器必须验证其返回的值，因为 CADRS 不会这样做。
- 3. 处理器必须将值作为列表的第一个元素返回（在本例中通过 `(ncons newvalue)`）。

1984年7月3日

### 10.3.2 cadrs-except-type?-nostruc 示例

这里使用异常处理程序重新回顾了关于类型和 `type?` 章节中的示例。

```
(structure person
  fields ((declare name is-a name)
    age
    sex))

(defun type?-women (form list structure)
  (if and
      (eq structure 'women)
          (memq 'person (type form))
      then (ncons (eq (fetch form sex) 'female))
      else nil))
```

```
(establish cadrs-except-type?-nostruc 'type?-women)

(type? (create person (sex .female) (woman)) => t
```

再次注意，`type?-women` 检查它正在处理的异常是否针对女性结构体^1，并使用 `ncons` 将该值作为列表的第一个元素返回。

1. 这一次 `women` 没有被定义为结构体

1984年7月3日

# 11 - CADRS 工具包

本章描述了为版本 1.00 提供的工具包。包括：

- 1. 针对 Franz Lisp 版本 1.00 的验证脚本。
- 2. CADRS 的重置函数。
- 3. 一个提供 `fetch` 和 `replace` 简写形式的语法宏。
- 4. 其他有用函数。

## 11.1 CADRSVAL

CADRSVAL 包提供了一系列函数，用于测试 CADRS 的每项功能。[[尚未完成]]

## 11.2

`cadrs-reset` 函数（目前位于 `CADRSTS.L` 中）将移除所有当前定义的结构。该函数的调用方式为：

```
(cadrs-reset)
```

## 11.3 RPM

由宾州大学的 Tim Finin 编写的 RPM 包为编写 `fetch` 和 `replace` 语句提供了简写形式。一旦用 CADRS 加载 RPM，将接受以下构造：

1984年7月3日

- 1. `#struct.path`
  这将其展开为 `(fetch struct path)`
- 2. `#struct.path=newval`
  这将其展开为 `(replace struct path newval)`

## 11.4 CADRSUTIL

CADRSUTIL 提供了一组函数，帮助对 CADRS 结构以及使用这些结构的函数进行调试和测试。每个函数描述如下：

### 11.4.1 structures

`structures` 是一个不带参数的函数，将显示当前定义的结构列表。

### 11.4.2 dump-field

`dump-field` 将显示与给定结构相关的字段当前属性值。格式为：

```
(dump-field field struc)
```

其中：

- `field` - 要转出的字段名称。
- `struct` - 包含该字段的结构。

### 11.4.3 dump-structure

`dump-structure` - 显示给定结构的所有属性。格式为：

```
(dump-structure struc)
```

其中：

- `struc` - 要转出的结构。

### 11.4.4 dump-all-structures

这是一个不带参数的函数，它会转储所有当前定义的结构的属性值。

### 11.4.5 edits

`edits` 函数使用 LISP 编辑函数来修改 LISP 环境中的结构定义。格式为：

```
(edits struc)
```

其中：

- `struc` - 要编辑的结构。

1984年7月3日

# 12 - 结论

## 12.1 结语

通过对传统结构定义形式的扩展，CADRS 在高效实现中体现了面向对象系统的许多优势。该包具有许多其他基于 LISP 的结构定义包中未发现的功能，包括从网络表示方案中引入的功能。

## 12.2 未来工作

CADRS 正在考虑若干项新增，包括：

- i. 一种更灵活的（类英语的）结构定义语言，以取代严谨的属性/值语法。
- ii. 结合 (i) 构建一种更健壮的访问机制，以处理数据路径推理、数据路径的运行时规范，以及作为路径的一部分指定结构类型以消除歧义¹。
- iii. 可能结合 (i) 和 (ii) 构建一个带类型的函数形式体系（类似于 GLISP）。
- iv. 构建一个消息机制，允许更完整的以对象为中心的编程。
- v. 添加一个销毁函数来销毁结构实例（如果 CADRS 将用于数据库研究，这是必要的）。
- vi. 一种（COBOL 意义上的）重新定义结构部分的方法。

> 1. 这些歧义目前出现在当 2 个结构对同一字段有“不同”定义时。这种情况通过在执行字段访问时对实例进行类型检查来解决。

1984年7月3日

## 参考文献

- 1. Bawden, Alan. "DEFSTRUCT Reference Documentation." Massachusetts Institute of Technology (ALANEMC), 1980
- 2. Birtistle, G., Dahl, O., Myhrgaard, B., and Nygaard, K. Simula Begin. Petrocelli/Carter, 1975.
- 3. Mylopopoulos, John. "An Overview of Knowledge Representation." The Proceedings of the Workshop on Data Abstractions, Databases and Conceptual Modelling (SIGPLAM), January 1981.
- 4. Novak, Gordon S. "CLISP User’s Manual." Stanford University, Stanford California, 1982.
- 5. Roberts, Bruce R., and Goldstein, Ira P. The FRL Manual. MIT AI Memo 409, September 1977
- 6. Steengaard-Madsen, J. "A Statement-Oriented Approach to Data Abstraction." Communications of the ACM. January, 1981.
- 7. Stroustrup, Bjarne. "Classes: An Abstract Data Type Facility for the C Language." Special Interest Group for Programming Languages (SIGPLAN) Notices. January 1982
- 8. Teitman, Warren. The INTERISP Reference Manual; Bolt, Beranek & Newman - Xerox Corporation, 1978.
- 9. Worth, Niklaus. Algorithms + Data Structures = Programs; Prentice Hall, 1976.
