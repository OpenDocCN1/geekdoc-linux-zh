
- IDL Mapping for Python (http://www.python.org/sigs/do).
- IDL Mapping for Erlang (http://www.erlang.org/doc/lib/orber-2.0).
- CORBA support for Haskell (http://cse.unsw.edu.au/~chak/gnome/node11.html).
- CORBA Mapping for Perl. (http://people.redhat.com/otaylor/corba/mapping.html#CORBA_mapping_for_Perl)
- corba.el (http://www.lysator.liu.se/-lenst/corba.el) an Emacs client-side implementation of CORBA.

```
interface FACTORY {
MEMBERSHIP MEMBERSHIP();
TITLING TITLING();
DISKS DISKS();
RENTALS RENTAL();
RESERVATIONS RESERVATIONS();
UTILITIES UTILITIES();
```

# IDL 类型到 C 类型映射

| IDL 类型 | C 类型映射 |
| :--- | :--- |
| float | CORBA_float |
| double | CORBA_double |
| long double | CORBA_long_double |
| boolean | CORBA_boolean |
| char | CORBA_char |
| wchar | CORBA_wchar |

程序并没有直接使用 `some_long_variable`，而是使用 `CORBA_long some_long_variable`。这导致了 CORBA 所需的特定类型，而不是将选择权交给 C 实现去应用。在普通的 IA-32 系统上，这个问题可能并不十分重要，因为基础 C 类型与 CORBA 类型基本一致；但随着我们向 64 位架构迈进，这将成为一个严重的问题，因为“原生”类型倾向于 64 位宽。

因此，对于接口 `MEMBERSHIP` 中的 `typedef long memberid;`，我们得到：

```c
typedef CORBA_long DVD_MEMBERSHIP_memberid;
```

对于接口 `TITLING` 中的 `typedef long titleid;`，我们得到：

```c
typedef CORBA_long DVD_TITLING_titleid;
```

# 构造与模板数据类型

映射包括：

## 字符串

考虑日期字符串类型：

```c
typedef string datec;
```

该定义的 C 语言映射为：

```c
typedef CORBA_char *DVD_datec;
```

这反映了 C 字符串只是字符数组。

## 结构体

这里的映射并不意外。例如，模块 `DVD` 中接口 `MEMBERSHIP` 的 `struct:embermembers` 的 IDL 定义如下：

```c
struct storemembers (
    memberid memberid;    /* 内部 ID [1..] */
    string memberno;      /* 成员知的编号 */
```

# 第 20 章

```c
/* Mr Mrs Ms Dr Sir */
string title; /* 头衔 */
string fname; /* 姓 */
string lname;
string houseffret; /* 例如 5，或 'The birches' 等. */
string address; /* 地址行 1 */
string address2; /* 地址行 2 */
string town; /* 城镇/城市 */
string state; /* 仅美国需要 */
string phone; /* +44(0)123 456789 */
string zipcode; /* LEI 1AA 或其他 */
```

这被映射到以下 C 结构体：

```c
typedef struct {
    DVD_MEMBERSHIP_memberid memberid;
    CORBA_char *membername;
    CORBA_char *title;
    CORBA_char *fname;
    CORBA_char *lname;
    CORBA_char *houseffret;
    CORBA_char *address1;
    CORBA_char *address2;
    CORBA_char *town;
    CORBA_char *state;
    CORBA_char *phone;
    CORBA_char *zipcode;
} DVD_MEMBERSHIP_storemembers;
```

模块、接口和结构体的名称拼接在一起得到 C 名称：

`DVD_MEMBERSHIP_storemembers`

## 序列 (Sequences)

结构体生成中的序列用于将各个组件收集成一个数组。例如，接口 `MEMBERSHIP` 声明了一个序列成员 `memberId`：

```c
typedef sequence<memberid> memberList;
```

这会导致生成以下结构体：

```c
typedef struct {
    CORBA_unsigned_long _maximum;
```

它允许包含序列中允许的最大元素数量：

```c
    _length;
```

`length` 是一个强制性元素，代表传递到序列中的条目数：

```c
DVD_MEMBERSHIP_memberid *buffer;
```

```c
CORBA_boolean _release;
```

`_release` 是一个变量，指示数据传输完成后 ORB 是否应该释放序列信息：

```c
CORBA_sequence_DVD_MEMBERSHIP_memberid;
```

为了使用此项，你可能会编写如下代码：

```c
/* 设置序列变量 */
CORBA_sequence_DVD_MEMBERSHIP_memberid membs;
/* 在序列中分配条目 */
membs_buffer = CORBA_alloc_DVD_MEMBERSHIP_memberid(6);
membs_length = 6; /* 猜猜我们有多少个条目？ */
membs_buffer[0] = member1;
membs_buffer[1] = member2;
membs_buffer[2] = member3;
membs_buffer[3] = member4;
membs_buffer[4] = member5;
membs_buffer[5] = member6;
```

这提供了 `membs`，准备好作为参数传递给服务器，或作为结果返回给客户端。

## 枚举 (Enumerations)

这不是 DVD 应用的示例，但本可以是：

```c
enum emovierratings (G, PG13, NC17, R, NR, XXX);
```

这可以映射到：

## 数组 (Arrays)

查看：

```c
typedef double memid[8][12];
```

我们得到定义：

```c
typedef double DVD_memid[8][12];
typedef CORBA_double DVD_memid_slice[12];
```

切（slices）代表数组的“次部分”，如果你愿意，可以单独分配它们。

# 第 20 章

## 常量引用 (Constant References)

这种映射允许在 IDL 中定义常量并在 C 中使用。然而，IDL 没有直接的“常量”类型；相反，常量通过枚举或在 C 代码中使用预处理器宏来处理。（注意：与其他语言不同，标准 IDL 并没有全局 `const` 关键字）。

## CORBA

### 异常处理 (Exception Handling)

这是映射到 C 特别笨拙的领域之一。IDL 定义的结构化异常系统与 C++ 异常系统相当。C 在这方面缺失。因此，C 映射涉及为每个方法添加额外的返回值“异常环境”，程序必须解释该环境。你可能会想要构建只使用一两次原生映射的辅助函数。

假设我们声明了如下异常：

```idl
module main {
    exception foo (); // 无参数异常
    interface secondary {
        exception bar ( // 带参数异常
            string msg;
        )
    };
}
```

C 语言映射产生以下声明：
