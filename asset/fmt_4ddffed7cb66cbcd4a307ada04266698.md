
关于使用 `static` 关键字有一些重要的注意事项。首先，不要使用 `$this->varName` 语法从类内部访问变量，而应使用 `self::$varName`。在之前的示例中，你从一个不同的函数中访问了 `self::$count` 成员，但由于静态成员对类内部的一切都可用，因此仍然使用了 `self::` 语法。其次，当从类外部访问静态成员时，应使用语法 `className::$varName`。同样，当在类内部任何地方访问静态方法时，应使用 `self::methodName()`；当从类外部访问时，应使用 `className::methodName()`。

关于使用 `static` 关键字的更详细讨论将在第 2 章中进行。

### abstract 关键字

当你有一个高级类，知道它将被更具体、更低的类继承时，使用 abstract 关键字。例如，你可以如下使用抽象类和方法：

```php
<?php
    abstract class getToday {
        public $today = getdate();
        abstract function showCalendar();
    }
    class monthlyCalendar extends getToday {
        function showCalendar() {
            //显示本月的日历
        }
    }
    class dailyCalendar extends getToday {
        function showCalendar() {
            //显示今天的每日日历
        }
    }
    class yearlyCalendar extends getToday {
        function showCalendar() {
            //显示今年的日历
        }
    }
?>
```

这个抽象类基本上说“创建一个日历，但然后在子类中指定其类型”。如你所见，第一个类中的 `showCalendar()` 函数被故意留空并设为抽象，因为该类应该被扩展，并根据调用的继承类显示适当的日历。`getToday()` 类是不完整的，是抽象化的完美候选者。抽象方法（如同接口中的方法）实际上是空的，需要在子类中进一步实现。

使用抽象类时的一些规则包括：

- 如果你有抽象方法，整个类也必须定义为抽象。
- 你不能实例化抽象类。
- 你可以将一个类定义为抽象类，即使它不包含任何抽象方法。
- 实现抽象方法的继承类必须具有与其父类相同（或更弱）的可见性。

在第 2 章中，我们将更详细地讨论抽象。

### 内置方法重载函数

与 PHP4 不同，在 PHP4 中你必须使用 `overload()` 函数来强制进行重载检查，而 PHP5 原生允许你对任何不符合预期的方法或成员引用进行重载，从而有效地让你控制接下来发生的事情。新的魔术方法 `__get()`、`__set()` 和 `__call()` 用于重载，如下所示：

```php
<?php

class overload {

  function __get($property) {
    //检查属性是否存在于类中
    //如果不存在，执行我们想要执行的操作
    //例如显示错误。否则返回
    //一个值。
  }

  function __set($property, $value) {
    //检查属性是否存在于类中
    //如果存在，将其设置为传入的值
    //否则执行我们想要执行的操作，例如
    //显示错误。
  }

  function __call($method, $array_of_arguments) {
    //检查方法是否存在于类中
    //如果不存在，执行某些操作，例如将其委托给
    //包含该方法的另一个类或
    //打印错误语句。
  }
}
?>
```

第 2 章将更详细地讨论重载。

### 新函数

以下是 PHP5 中所有新函数的综合列表，不包括那些需要扩展的函数：

- `array_combine()`: 将两个数组合并为一个，使用其中一个数组作为值，另一个数组作为键。
- `array_diff_uassoc()`: 通过命名字典确定两个或多个数组之间的差异，并进行额外的键比较。
- `array_udiff()`: 通过使用命名字典进行数据比较，确定两个或多个数组之间的差异。
- `array_udiff_assoc()`: 通过使用命名字典进行数据比较，并进行额外的键比较，确定两个或多个数组之间的差异。
- `array_udiff_uassoc()`: 通过使用命名字典进行额外的键比较，以及通过命名字典进行数据比较，确定两个或多个数组之间的差异。
- `array_intersect()`: 通过使用命名字典进行数据比较，确定两个或多个数组之间的交集。
- `array_intersect_assoc()`: 通过使用命名字典进行数据比较，并进行额外的键比较，确定两个或多个数组之间的交集。
- `array_intersect_uassoc()`: 通过使用命名字典进行额外的键比较，以及通过命名字典进行数据比较，确定两个或多个数组之间的交集。
- `array_walk_recursive()`: 对数组的每个元素递归地应用命名字典。
- `convert_uudecode()`: 解码 uuencoded 字符串。
- `convert_uuencode()`: 对字符串进行 uuencode 编码。
- `curl_copy_handle()`: 复制 cURL 句柄及其所有偏好设置。
- `date_sunrise()`: 基于给定的纬度、经度、天顶角和 GMT 偏移量返回日出时间。
- `date_sunset()`: 基于给定的纬度、经度、天顶角和 GMT 偏移量返回日落时间。
- `dba_key_split()`: 将字符串表示中的索引拆分为数组表示。
- `dbase_get_header_info()`: 返回 dBase 数据库的列结构信息。

# 第 1 章

- `dbx_fetch_row()`: 从查询结果中获取行，但如果查询中未设置 DBX_RESULT_UNBUFFERED，则执行将失败。
- `fbsql_set_password()`: 更改指定用户的密码。
- `file_put_contents()`: 等效于打开文件、写入文件并关闭文件的操作。
- `ftp_alloc()`: 向 FTP 服务器发送 ALLO 命令，该命令为上传文件预留空间。
- `get_declared_interfaces()`: 返回脚本中已声明的任何接口。
- `get_headers()`: 返回服务器响应 HTTP 请求时发送的头部信息。
- `headers_list()`: 返回已发送（或准备发送）的响应头列表。
- `http_build_query()`: 根据给定的数组返回 URL 编码的查询字符串。
- `ibase_affected_rows()`: 返回受上一个查询影响的行数（Interbase）。
- `ibase_backup()`: 在服务管理器中启动备份任务并立即返回（Interbase）。
- `ibase_commit_ret()`: 提交事务，但不关闭它然后返回（Interbase）。
- `ibase_db_info()`: 返回关于数据库的信息（Interbase）。
- `ibase_drop_db()`: 删除数据库（Interbase）。
- `ibase_errcode()`: 返回错误代码（Interbase）。
- `ibase_free_event_handler()`: 释放已注册的事件处理程序（Interbase）。
- `ibase_gen_id()`: 增量增加并返回增加后的值（Interbase）。
- `ibase_maintain_db()`: 在数据库服务器上执行维护命令（Interbase）。
- `ibase_name_result()`: 为结果集命名（Interbase）。
- `ibase_num_params()`: 返回命名查询中的参数数量（Interbase）。
- `ibase_param_info()`: 返回命名查询的参数信息（Interbase）。
- `ibase_restore()`: 在服务管理器中启动恢复任务并立即返回（Interbase）。
- `ibase_rollback_ret()`: 回滚事务但不关闭它（Interbase）。
- `ibase_server_info()`: 返回关于数据库的信息（Interbase）。
- `ibase_service_attach()`: 连接到服务管理器（Interbase）。
- `ibase_service_detach()`: 断开与服务管理器的连接（Interbase）。
